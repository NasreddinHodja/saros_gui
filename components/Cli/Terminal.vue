<script setup lang="ts">
interface Command {
  command: string;
  output: string;
}

const emit = defineEmits<{
  (event: "draw", count: number): void;
  (event: "clear"): void;
}>();

const history = ref<Command[]>([]);

const promptRef = useTemplateRef("prompt-ref");

const handleClick = () => {
  if (promptRef.value?.inputRef) {
    promptRef.value.inputRef.focus();
  }
};

const executeCommand = (command: string): Command => {
  const commandParts = command.trim().split(" ");
  if (commandParts[0] === "draw") {
    if (commandParts.length === 1) {
      emit("draw", 1);
      return { command, output: "Drawing 1 card..." };
    } else {
      const number = parseInt(commandParts[1]);

      if (isNaN(number)) {
        return { command, output: "Error: Invalid number." };
      } else if (number >= 1 && number <= 5) {
        emit("draw", number);
        return {
          command,
          output: `Drawing ${number} card${number === 1 ? "" : "s"}...`,
        };
      } else {
        return { command, output: "Drawing number must be between 1 and 5." };
      }
    }
  } else if (commandParts[0] === "clear") {
    emit("clear");
    return { command, output: "Clearing drawed cards." };
  } else if (commandParts[0] === "help") {
    return {
      command,
      output: `
Available Commands:
- draw [number]: Draws the specified number of cards (1 to 5).
  Example: "draw 3" will draw 3 cards.
- clear: Clears drawed cards.
- help: Displays this help message.
    `,
    };
  }
  return {
    command,
    output:
      "Error: command not found.\nInput 'help' to see available commands.",
  };
};

const handleCommand = (command: string) => {
  history.value.push(executeCommand(command));
  nextTick(() => {
    const container = document.getElementById("container");
    if (container) {
      container.scrollTop = container.scrollHeight;
    }
  });
};
</script>

<template>
  <div
    id="container"
    class="flex flex-col gap-2 border-4 h-1/4 w-1/2 items-start justify-start p-5 overflow-hidden"
    @click="handleClick"
  >
    <div v-for="historyItem in history" class="flex flex-col">
      <span class="font-mono">>&nbsp;{{ historyItem.command }}</span>
      <pre class="font-mono">{{ historyItem.output }}</pre>
    </div>

    <CliPrompt ref="prompt-ref" @command="handleCommand" />
  </div>
</template>
