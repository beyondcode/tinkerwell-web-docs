# Tinkerwell Web Documentation

This repository holds the [Tinkerwell Web](https://web.tinkerwell.app) documentation for Laravel. 

To include code snippet buttons into the documentation, place them in a code block that looks like this:

	```try-code
	{
		mode: 'cli',
		cliCode: `collect(range(1,50));`
	}
	```
	
This will automatically render a button that, once pressed, executes the code and displays the result to the user.
	
## Available modes

The code snippet buttons can trigger two different modes. The `http` mode, which will show a controller editor, a view editor and the output in form of an iFrame / HTML.

Or the `cli` mode, which displays one editor on the left and the code output on the right.

## CLI

The `cli` mode object has the following structure:

	```try-code
	{
		mode: 'cli',
		cliCode: `your-code-snippet-goes-here`
	}
	```
	
	

## HTTP

The `http` mode object has the following structure:

	```try-code
	{
		mode: 'http',
		controllerCode: `controller code`,
		viewCode: `view code`
	}
	```