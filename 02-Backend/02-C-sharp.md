The C# programming language allows you to build many types of applications, like:
	- Business applications to capture, analyze, and process data
	- Dynamic web applications that can be accessed from a web browser
	- Games, both 2D and 3D
	- Financial and scientific applications
	- Cloud-based applications
	- Mobile applications       
First Code
```C#
Console.WriteLine("Hello World!");
```
First Program
```C#
Console.Write("Congratulations!");
Console.Write(" ");
Console.Write("You wrote your first lines of code.");
```
 The difference between Console.Write and Console.WriteLine
	 `Console.WriteLine()` prints a message to the output console. At the end of the line, it adds a line feed similar to pressing Enter or Return to create a new line.
	To print to the output console, but without adding a line feed at the end, you use the second technique, `Console.Write()`. So, the next call to `Console.Write()` prints another message to the same line.
```C#
Console.WriteLine("Congratulations!");
Console.Write("You wrote your first lines of code.");
```