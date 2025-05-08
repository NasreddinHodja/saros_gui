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
      return { command, output: "Tirando 1 carta..." };
    } else {
      const number = parseInt(commandParts[1]);

      if (isNaN(number)) {
        return { command, output: "Erro: Número inválido." };
      } else if (number >= 1 && number <= 5) {
        emit("draw", number);
        return {
          command,
          output: `Drawing ${number} card${number === 1 ? "" : "s"}...`,
        };
      } else {
        return { command, output: "O número de cartas deve ser entre 1 e 5." };
      }
    }
  } else if (commandParts[0] === "clear") {
    history.value = [];
    emit("clear");
    return { command, output: "Limpando a tela..." };
  } else if (commandParts[0] === "help") {
    return {
      command,
      output: `
Comandos disponíveis:
- draw [número]: Tira o número especificado de cartas (de 1 a 5).
  Exemplo: "draw 3" irá tirar 3 cartas.
- clear: Limpa as cartas tiradas.
- help: Exibe esta mensagem de ajuda.
    `,
    };
  }
  return {
    command,
    output:
      "Erro: comando não encontrado.\nDigite 'help' para ver os comandos disponíveis.",
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
    class="flex flex-col gap-2 border-4 h-2/6 w-3/5 items-start justify-start p-5 overflow-hidden"
    @click="handleClick"
  >
    <div v-for="historyItem in history" class="flex flex-col">
      <span class="font-mono">>&nbsp;{{ historyItem.command }}</span>
      <pre class="font-mono">{{ historyItem.output }}</pre>
    </div>

    <CliPrompt ref="prompt-ref" @command="handleCommand" />
  </div>
</template>
