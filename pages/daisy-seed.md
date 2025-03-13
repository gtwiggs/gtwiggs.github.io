# daisy-synth-notes

Learning new software, hardware and concepts requires lots of research and sifting through what is interesting. These notes collect what interests me.

## DaisySeed

### Projects of Interest

- [DaisySeed Pinout](https://images.squarespace-cdn.com/content/v1/58d03fdc1b10e3bf442567b8/1638921637961-UEMNQ2S8CS4V1M040IVQ/Daisy_Seed_pinout.png)
- [libDaisy](https://electro-smith.github.io/libDaisy/index.html) ~ C++ hardware support library
- [My fork of Synthux-Academy/simple-designer-instruments](https://github.com/gtwiggs/simple-designer-instruments/tree/main)

### Debugger Probe

- [Setting up VSCode/OpenOCD (XPack)/ST-Link for debugging on MacOS Big Sur](https://forum.pedalpcb.com/threads/setting-up-vscode-openocd-xpack-st-link-for-debugging-on-macos-big-sur.4861/) ~ (works on macos Sonoma as well) ST-Link is a debugging probe for the Daisy Seed.
- Revised `launch.json` that enables `liveWatch` & replaces deprecated `runToMain` with `runToEntryPoint`:
```json
{
    // Use IntelliSense to learn about possible attributes.
    // Hover to view descriptions of existing attributes.
    // For more information, visit: https://go.microsoft.com/fwlink/?linkid=830387
    "version": "0.2.0",
    "configurations": [
        {
            "name": "Cortex Debug",
            "cwd": "${workspaceRoot}",
            "executable": "build/FeedbackSynth.elf",
            "request": "launch",
            "type": "cortex-debug",
            "servertype": "openocd",
            "configFiles": ["interface/stlink.cfg", "target/stm32h7x.cfg"],
            "openOCDLaunchCommands": ["init", "reset init"],
            "runToEntryPoint": "main",
            "liveWatch": { "enabled": true, "samplesPerSecond": 4 },
            "svdFile": "./.vscode/STM32H750x.svd"
        }
    ]

}
```
- To use ST-Link:
    - Compile and upload from VSCode: `CMD-P task build_and_program`
    - [Start a debug session](https://code.visualstudio.com/docs/editor/debugging#_launch-configurations) selecting `Cortex Debug` and clicking the adjacent green ***>*** to start.
    - Debug session must be terminated to upload changes.
    - When plugging in the ribbon cable, ensure the cable is inserted with the ribbon routed **_up_** when the USB port is to the left.

### DaisySeed <> PureData

- [Daisy Forum dedicated to Pure Data projects on a Daisy Seed](https://forum.electro-smith.com/t/pure-data/110)
- [pd2dsy](https://github.com/electro-smith/pd2dsy)

## PureData

- [Pd Download](http://msp.ucsd.edu/software.html) and [Manual](http://msp.ucsd.edu/Pd_documentation/index.htm)
- [pd-else](https://github.com/porres/pd-else/?tab=readme-ov-file) ~ ELSE is a big library of externals that extends the performance Pure Data (Pd). ELSE provides a cohesive system for computer music, it also serves as a basis for an [Live Electronics Tutorial]().
- [MIT Press Code examples for “Designing Sound” textbook](https://mitp-content-server.mit.edu/books/content/sectbyfn/books_pres_0/8375/designing_sound.zip/chapter09.html)

## Sound Synthesis

- [Physical Modelling Synthesis](https://ccrma.stanford.edu/software/clm/compmus/clm-tutorials/pm.html) ~ _... physical modeling it is the actual physics of the instrument and its playing technique which are modelled by the computer._
- [The Synthesis ToolKit in C++ (STK)](https://ccrma.stanford.edu/software/stk/) _is a set of open source audio signal processing and algorithmic synthesis classes ..._ I found thiis by searching for by Gary P. Scavone who was mentioned in a (lost) video on DaisySeed sound synthesis, I think relating to the Audrey II project from Synthux Academy.
