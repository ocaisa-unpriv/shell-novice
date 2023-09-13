---
title: Introducción al Shell
teaching: 5
exercises: 0
---

::::::::::::::::::::::::::::::::::::::: objectives

- Explique cómo se relaciona el shell con el teclado, la pantalla, el sistema operativo y los programas de los usuarios.
- Explicar cuándo y por qué las interfaces de línea de comandos deben ser usadas en lugar de las interfaces gráficas.

:::::::::::::::::::::::::::::::::::::::::::::::
:::

:::::::::::::::::::::::::::::::::::::::: questions

- ¿Qué es un shell de comandos y por qué utilizaría uno?

:::::::::::::::::::::::::::::::::::::::::::::::
:::

### Contexto

Los seres humanos y las computadoras suelen interactuar de muchas maneras diferentes, como a través de un teclado y ratón, interfaces, de pantalla táctil o usando sistemas de reconocimiento de voz. La forma más utilizada para interactuar con ordenadores personales se llama **interfaz gráfica de usuario** (GUI). Con un GUI, damos instrucciones haciendo clic en el ratón y usando interacciones guiadas por menús.

Mientras que la ayuda visual de un GUI hace intuitivo aprender, esta forma de entregar instrucciones a un ordenador se escala muy mal. Imagine la siguiente tarea: para una búsqueda de literatura, tienes que copiar la tercera línea de mil archivos de texto en mil directorios diferentes y pegarlo en un solo archivo. Usando una interfaz GUI, no sólo haría clic en su escritorio durante varias horas, pero potencialmente también podría cometer un error en el proceso de completar esta tarea repetitiva. Aquí es donde aprovechamos el shell de Unix. The Unix shell is both a **command-line interface** (CLI) and a scripting language, allowing such repetitive tasks to be done automatically and fast. With the proper commands, the shell can repeat tasks with or without some modification as many times as we want. Using the shell, the task in the literature example can be accomplished in seconds.

### The Shell

The shell is a program where users can type commands. With the shell, it's possible to invoke complicated programs like climate modeling software or simple commands that create an empty directory with only one line of code. La terminal más popular de Unix se llama **Bash**, que proviene de **Bourne Again Shell** (así llamada porque deriva de una versión previa escrita por Stephen Bourne). **Bash** es la terminal por defecto en la mayoría de las implementaciones modernas de Unix, y en la mayoría de los paquetes que proporcionan herramientas similares a las de Unix para Windows. Note that 'Git Bash' is a piece of software that enables Windows users to use a Bash like interface when interacting with Git.

Using the shell will take some effort and some time to learn. While a GUI presents you with choices to select, CLI choices are not automatically presented to you, so you must learn a few commands like new vocabulary in a language you're studying. However, unlike a spoken language, a small number of "words" (i.e. commands) gets you a long way, and we'll cover those essential few today.

Por otra parte, con unas cuantas teclas la terminal nos permite combinar las herramientas existentes en potentes **pipelines** y manejar grandes volúmenes de datos automáticamente. Sequences of commands can be written into a *script*, improving the reproducibility of workflows.

Además, la línea de comandos es a menudo la forma más fácil de interactuar con máquinas remotas y superordenadores. La familiaridad con la terminal es casi esencial para utilizar una variedad de herramientas y recursos especializados, incluyendo sistemas de computación de alto rendimiento. A medida que los **clusters** y los sistemas de computación en la nube se vuelven más populares para el análisis de datos científicos, ser capaz de interactuar con ellos se convierte en una habilidad necesaria. Podemos aprovechar las habilidades que adquiriremos en línea de comandos para abordar una amplia gama de preguntas científicas y desafíos computacionales.

Let's get started.

When the shell is first opened, you are presented with a **prompt**, indicating that the shell is waiting for input.

```bash
$
```

El shell normalmente usa `$` como indicación, pero puede usar un símbolo diferente. In the examples for this lesson, we'll show the prompt as `$`. Most importantly, *do not type the prompt* when typing commands. Only type the command that follows the prompt. This rule applies both in these lessons and in lessons from other sources. Also note that after you type a command, you have to press the <kbd>Enter</kbd> key to execute it.

The prompt is followed by a **text cursor**, a character that indicates the position where your typing will appear. The cursor is usually a flashing or solid block, but it can also be an underscore or a pipe. You may have seen it in a text editor program, for example.

Note that your prompt might look a little different. In particular, most popular shell environments by default put your user name and the host name before the `$`. Such a prompt might look like, e.g.:

```bash
nelle@localhost $
```

The prompt might even include more than this. Do not worry if your prompt is not just a short `$`. This lesson does not depend on this additional information and it should also not get in your way. The only important item to focus on is the `$` character itself and we will see later why.

So let's try our first command, `ls`, which is short for listing. This command will list the contents of the current directory:

```bash
$ ls
```

```output
Desktop     Downloads   Movies      Pictures
Documents   Library     Music       Public
```

:::::::::::::::::::::::::::::::::::::::::  callout

## Command not found

If the shell can't find a program whose name is the command you typed, it will print an error message such as:

```bash
$ ks
```

```output
ks: command not found
```

Esto puede suceder si el comando fue mal escrito o si el programa correspondiente a ese comando no está instalado.


:::::::::::::::::::::::::::::::::::::::::::::::
:::

## Pipeline de Nelle: Un problema típico

Nelle Nemo, una bióloga marina, acaba de regresar de un estudio de seis meses del [Giro del Pacífico Norte](https://en.wikipedia.org/wiki/North_Pacific_Gyre), en donde ha estado muestreando la vida marina gelatinosa en la [Gran Mancha de Basura del Pacífico](https://en.wikipedia.org/wiki/Great_Pacific_Garbage_Patch). She has 1520 samples that she's run through an assay machine to measure the relative abundance of 300 proteins. She needs to run these 1520 files through an imaginary program called `goostats.sh`. In addition to this huge task, she has to write up results by the end of the month, so her paper can appear in a special issue of *Aquatic Goo Letters*.

If Nelle chooses to run `goostats.sh` by hand using a GUI, she'll have to select and open a file 1520 times. If `goostats.sh` takes 30 seconds to run each file, the whole process will take more than 12 hours of Nelle's attention. With the shell, Nelle can instead assign her computer this mundane task while she focuses her attention on writing her paper.

The next few lessons will explore the ways Nelle can achieve this. More specifically, the lessons explain how she can use a command shell to run the `goostats.sh` program, using loops to automate the repetitive steps of entering file names, so that her computer can work while she writes her paper.

As a bonus, once she has put a processing pipeline together, she will be able to use it again whenever she collects more data.

In order to achieve her task, Nelle needs to know how to:

- navigate to a file/directory
- create a file/directory
- check the length of a file
- chain commands together
- retrieve a set of files
- iterate over files
- run a shell script containing her pipeline



:::::::::::::::::::::::::::::::::::::::: keypoints

- Un intérprete de comandos es un programa cuyo propósito principal es leer comandos y ejecutar otros programas.
- Esta lección utiliza Bash, el intérprete de comandos predeterminado en muchas implementaciones de Unix.
- Programs can be run in Bash by entering commands at the command-line prompt.
- Las principales ventajas de la terminal son su alta relación acción-tecla, su soporte para la automatización de tareas repetitivas, y que puede utilizarse para acceder a otras máquinas en una red.
- A significant challenge when using the shell can be knowing what commands need to be run and how to run them.

:::::::::::::::::::::::::::::::::::::::::::::::
:::


