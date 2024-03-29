# HecateEngine Setup Guide for macOS

This guide will walk you through setting up the required tools and configurations for the HecateEngine project on macOS.

## Table of Contents

1. [Install Homebrew](#install-homebrew)
2. [Install CMake](#install-cmake)
3. [Visual Studio Code Configuration](#visual-studio-code-configuration)
   - [Launch Configuration](#launch-configuration)
   - [Settings](#settings)
   - [Tasks](#tasks)

---

## Install Homebrew

[Homebrew](https://brew.sh/) is a package manager for macOS that simplifies the installation of software and tools.

To install Homebrew, open Terminal and execute the following command:

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

Follow the on-screen instructions to complete the installation.

---

## Install CMake

[CMake](https://cmake.org/) is a cross-platform tool designed to build, test, and package software.

Once you have Homebrew installed, you can install CMake using the following command:

```bash
brew install cmake
```

---

## Visual Studio Code Configuration

### Launch Configuration

Copy and paste the following configuration into your `.vscode/launch.json` file to set up the debug and release configurations for HecateEngine:

```json
{
  "version": "0.2.0",
  "configurations": [
    {
      "name": "Debug HecateEngine",
      "type": "cppdbg",
      "request": "launch",
      "program": "${workspaceFolder}/build/HecateEngine",
      "args": [],
      "stopAtEntry": false,
      "cwd": "${workspaceFolder}",
      "environment": [],
      "externalConsole": false,
      "MIMode": "lldb",
      "preLaunchTask": "Build HecateEngine Debug"
    },
    {
      "name": "Release HecateEngine",
      "type": "cppdbg",
      "request": "launch",
      "program": "${workspaceFolder}/build/HecateEngine",
      "args": [],
      "stopAtEntry": false,
      "cwd": "${workspaceFolder}",
      "environment": [],
      "externalConsole": false,
      "MIMode": "lldb",
      "preLaunchTask": "Build HecateEngine Release",
      "setupCommands": [
        {
          "description": "Disable Debugging Output",
          "text": "lldb run",
          "ignoreFailures": true
        }
      ]
    }
  ]
}
```

### Settings

You can add any specific settings or configurations for your HecateEngine project here.

```json
{
    // C++ configuration
    "editor.defaultFormatter": "ms-vscode.cpptools",
    "editor.formatOnSave": true,

    // C++ Formatting
    "C_Cpp.clang_format_sortIncludes": false,
    "C_Cpp.vcFormat.space.pointerReferenceAlignment": "left",
    "C_Cpp.vcFormat.newLine.beforeOpenBrace.block": "newLine",
    "C_Cpp.vcFormat.newLine.beforeOpenBrace.function": "newLine",
    "C_Cpp.vcFormat.newLine.beforeOpenBrace.namespace": "newLine",
    "C_Cpp.vcFormat.newLine.beforeOpenBrace.type": "newLine",
    "C_Cpp.formatting": "vcFormat",
    
    // File and folder settings
    "files.exclude": {
        "**/.git": true,
        "**/.svn": true,
        "**/.DS_Store": true,
        "build/": true,
        "bin/": true,
        "obj/": true
    },

    // Editor settings
    "editor.tabSize": 4,
    "editor.insertSpaces": true,
    "editor.detectIndentation": false,

    // IntelliSense settings
    "C_Cpp.intelliSenseEngine": "default",

    // Git settings
    "git.ignoreLimitWarning": true,
}
```

### Tasks

Copy and paste your tasks configuration into your `.vscode/tasks.json` file to define the build tasks for your HecateEngine project.

```json
{
    "version": "2.0.0",
    "tasks": [
      {
        "label": "Build HecateEngine Debug",
        "type": "shell",
        "command": "cmake",
        "args": [
          "--build",
          "./build",
          "--config",
          "Debug"
        ],
        "group": "build",
        "problemMatcher": "$gcc"
      },
      {
        "label": "Build HecateEngine Release",
        "type": "shell",
        "command": "cmake",
        "args": [
          "--build",
          "./build",
          "--config",
          "Release"
        ],
        "group": "build",
        "problemMatcher": "$gcc"
      },
      {
        "label": "Run HecateEngine",
        "type": "shell",
        "command": "./build/HecateEngine",
        "dependsOn": "Build HecateEngine Debug",
        "group": {
          "kind": "test",
          "isDefault": true
        },
        "problemMatcher": []
      },
      {
        "label": "Clean Build",
        "type": "shell",
        "command":[
            "rm -rf build &&",
            "mkdir build &&",
            "cd build &&",
            "cmake .."
        ],
        "group": "build",
        "problemMatcher": []
      }
    ]
}
```
