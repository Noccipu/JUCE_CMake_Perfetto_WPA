# JUCE - CMake - Perfetto - WPA template

This JUCE project template merges the [JUCE/examples/CMake/AudioPlugin](https://github.com/juce-framework/JUCE/tree/master/examples/CMake/AudioPlugin), the [Melatonin Perfetto](https://github.com/sudara/melatonin_perfetto) module and the [Windows Performance Analyzer (WPA)](https://learn.microsoft.com/fr-fr/windows-hardware/test/wpt/windows-performance-analyzer) to provide a comprehensive profiling solution tailored for advanced audio application development.


## Setup

### Built with
- Windows 11
- [Visual Studio Code](https://code.visualstudio.com/) (1.91.1)
- [CMake](https://cmake.org/) (3.30.1)

### Requirements
- Windows OS
- [Windows Performance Analyzer *(WPA)*](https://learn.microsoft.com/fr-fr/windows-hardware/test/wpt/windows-performance-analyzer) from the Windows ADK
- CMake

### Install Template
- First, you can **clone** the github repository to the location of your choice
```git 
git clone link
```

- The template requires the installation of two **submodules** ([JUCE](https://github.com/juce-framework/JUCE) and [Melatonin Perfetto](https://github.com/sudara/melatonin_perfetto))
```git
git submodule --init --recursive
```


## Usage

### Usage Overview
The template does several things, all of which can be customized: 

1. For a **Debug** build, you can toggle Melatonin Perfetto tracing via the `PERFETTO` CMake option:

```bash
cmake -B build -DCMAKE_BUILD_TYPE=Debug -DPERFETTO=ON
```

Once you set `PERFETTO=ON` (or `OFF`), that setting persists for subsequent CMake reconfigurations until you override it again.

2. For a **Debug** build, you can use a `launch.json` (*Debug and launch WPA*) configuration that runs Windows Performance Recorder (WPR) to capture CPU, GPU, memory, and other system events during the Standalone execution, then automatically opens the generated trace in Windows Performance Analyzer (WPA).

### Custom Usage
1. **`PERFETTO` MACRO**

It is possible to use a MACRO to neutralize certain portions of the code depending on whether or not the `PERFETTO` option is activated. This is done as follows:
```cpp
#ifdef PERFETTO
    TRACE_DSP();
#endif
```

2. **Custom Tracing** *(more info on the [Melatonin Perfetto repository](https://github.com/sudara/melatonin_perfetto?tab=readme-ov-file#step-2-pepper-around-some-sweet-sweet-trace-macros))*

The **tracing functions** in the template are the most basic versions of those available in the Melatonin Perfetto module. More information on the parameters of these functions is available in the project's GitHub repository.

3. **Custom WPR profiles** *(more info on the [Windows Hardware Developer documentation](https://learn.microsoft.com/en-us/windows-hardware/test/wpt/recording-with-custom-profiles))*

The default WPR profile is the **CPU profile**. However, it is possible to use other built-in profiles specified on the dedicated [WPR documentation](https://learn.microsoft.com/en-us/windows-hardware/test/wpt/built-in-recording-profiles) page. Modifications are made in the `/.vscode/tasks.json` file, in the *"Start WPA Recording"* task
```json
"args": [
    "-Command",
    "& { wpr -start CPU -filemode }"
],
```

It is also possible to add a custom profile, in which case you can modify the file `audio_plugin_profile.wprp` and replace the `CPU` in the command below.


## Documentation

### Useful Resources
- [CMake documentation](https://cmake.org/documentation/)
- [Melatonin Perfetto repository](https://github.com/sudara/melatonin_perfetto)
- [Perfetto documentation](https://perfetto.dev/docs/)
- [Windows Performance Analyzer documentation](https://learn.microsoft.com/en-us/windows-hardware/test/wpt/windows-performance-analyzer)
- [sudara Blog Post about Melatonin Perfetto](https://melatonin.dev/blog/using-perfetto-with-juce-for-dsp-and-ui-performance-tuning/)
- [JUCE repository](https://github.com/juce-framework/JUCE)
- [JUCE documentation](https://juce.com/)

### Useful Tools
- [Process Explorer](https://learn.microsoft.com/fr-fr/sysinternals/downloads/process-explorer) - A Windows utility that lets you see exactly which files, folders, and DLLs each running process has open.


## Project Status
This template was initially developed for a personal project requiring detailed and comprehensive performance analysis around a plugin developed with the JUCE framework for Windows. I thought it would be useful to share it with other users in the community who have the same **profiling** and **optimization** needs.

Any suggestions for **approaches**, **tools** or **code** are welcome, and I'd be delighted to make changes in the future!

Feel free to contact me on the server [Audio Programmer Discord](https://www.theaudioprogrammer.com/discord) or on the JUCE forum.


## License

[MIT](https://choosealicense.com/licenses/mit/)