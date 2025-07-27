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
        return {
          command,
          output: "Error: Number of cards must be between 1 and 5.",
        };
      }
    }
  } else if (commandParts[0] === "clear") {
    history.value = [];
    emit("clear");
    return { command, output: "Clearing screen..." };
  } else if (commandParts[0] === "help") {
    return {
      command,
      output: `
Available commands:
- draw [número]: 
  Draws specified number of cards 
  (from 1 to 5).
  Example: 
  "draw 3" will draw 3 cards.
- clear: 
  Clears the screen.
- help: 
  Shows this help message.`,
    };
  }
  return {
    command,
    output: "Error: command not found.\nType 'help' to see available commands.",
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
  <div class="w-full px-4 h-[65%] md:h-2/6 flex items-center justify-center">
    <div
      class="border-4 h-full w-full md:w-[700px] flex items-start justify-start p-5 text-white"
      @click="handleClick"
    >
      <div
        id="container"
        class="w-full h-full flex flex-col items-start justify-start overflow-hidden"
      >
        <div v-for="historyItem in history" class="flex flex-col w-full mb-4">
          <span class="font-mono text-wrap"
            >>&nbsp;{{ historyItem.command }}</span
          >
          <pre class="font-mono text-wrap">{{ historyItem.output }}</pre>
        </div>

        <CliPrompt ref="prompt-ref" @command="handleCommand" />
      </div>
    </div>
  </div>
</template>
