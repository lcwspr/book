# Getting Started With MASM and Visula Studio 2019

## Here's how to get started

1. irvine
2. Project32_VS2019
3. Project64_VS2019

## Required Setup for 32-bit Applications

1. select File -> new -> project -> c++
2. if you do not see visuall c++
   * close visual studio 
   * run a separate program named the visual studio installer
   * select the desktop development wtih c++ button
3. the visual c++ language includes the microsoft Assembler(MASM)
   * `c:\programfile\microsoft Visual Studio\2019\Community\VC\Tools\MSVC\14.xx\bin\Hostx64\x86`

## Setting up Visual Studio

1. Select the C++ Configuration
   1. Select Tools >> Import and Export Setting from the menu
   2. select the import selected environment settings radio button
   3. select the "No, just import..." radio button
   4. select "Visual C++" from the Default Setting List and click the Next button
   5. Click the finish button, then click the close button
   6. Notice the tabs on the left and right sides of the Visual Studio workspace.
      * close the server explorer, 
      * close the toolbox
      * close the properties tabs
      * you can use the mouse to drag the solution explorer tool window to the right side of the workspace.
2. Optional step: set the tab indent size
   1. select Options from the tools menu
   2. select and expand the text editor item,  
   3. select all languages, select tabs

## Tutorial: Building and running a 32-bit program

1. open a project

   1. VS requires assembly language source files to belong to a project, which is a kind of container. A project holds configuration information such as the locations of the assembler, linker, and required libraries. A project has tis own folder, and it holds the names and locations of all files belonging to it

   2. download a zip file containing an up-to-date project

   3. open project

      ```asm
      ; AddTwo.asm - adds two 32-bit integers
      ; Chapter 3 example
      
      .386
      .model flat,stdcall
      ExitProcess proto,dwExitCode:dword
      
      .code
      main proc
      	mov		eax, 5
      	add		eax, 6
      main endp
      end main
      ```

   4. add a file

      * Right-click the project name int the visual studio window, select add, select existing item
      * browse to the location of the file you want to add.

   5. build the program

      * assembel and link the sample program.
      * select build project from the build menu.

### Run the Program in Debug Mode

* The easiest way to run your first program is to use the debugger. First you must set a breakpoint. when you set a breakpoint in a program, you can use the debugger to execute the program a full speed(more or less) until it reaches the breakpoint. At that point, the debugger drops into single-step mode, 
  * omit
* when you assembled and linked the project, you can run it in the command prompt

### Registers

* you will want to display CPU registers when debugging your programs. 
  * first, under the tools >> options menu, select Debuging in the left panel, and select Enable address-level debugging. 
  * Netx, set a breakpoint, run your program in debug mode, 

## Tutorial: Building and running a 64-bit program

1. add the demo file

   ```asm
   ; AddTwoSum_64.asm - Chapter 3 example.
   ExitProcess proto
   
   .data 
   sum qword 0
   
   .code 
   main proc
   	mov rax, 5
   	add rax, 6
   	mov sum, rax
   	mov ecx, 0
   	call ExitProcess
   main endp
   end
   ```

## Building 16-bit programs

## Syntax highlighting in your source code

## visual studio compile

```asm
严重性	代码	说明	项目	文件	行	禁止显示状态
错误	MSB3721	命令“ml64.exe /c /nologo /Zi /Fo"x64\Debug\hello.obj" /W3 /errorReport:prompt  /Tahello.asm”已退出，返回代码为 1。	hello	D:\IDE\visualstudio\2019\Professional\MSBuild\Microsoft\VC\v160\BuildCustomizations\masm.targets	70	

```

