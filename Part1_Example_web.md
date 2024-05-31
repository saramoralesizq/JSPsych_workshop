# The basics of web programming
A webpage is usually built using three programming languages:
- HTML: This is used to create the structure of the webpage and present the static elements, such as text and multimedia content.
- CSS: This is used to style the content, but changing its appearance (size, position, etc.)
- JavaScript: This is used to allow people to interact with the webpage, changing its content based on time events (e.g., showing an image after 3 seconds) or people’s actions (clicking a button, pressing a key, moving the mouse, etc.)

# Creating a webpage. Hello world tutorial.
To create an empty webpage, create a new folder. Then create a new file inside the folder and save it as HTML. You can open this file with your browser and edit it using a code editor, such as Notepad ++ (available in the software centre in University-managed devices) or VSCode (free to download online). You can also use the normal Notepad in your device, but it is not very user friendly.
Once you have created your html file, you can copy paste this to create an empty webpage:
```
<!DOCTYPE html>
<html>
    <head>
        <title></title>
    </head>
    <body>
    </body>
</html>
```
All the content in HTML is placed in between tags. This would be an opening tag <> and this would be a closing tag </>.
A webpage has two main elements, the head and the body.
## Head
The head contains the links to other files. For example, if you have a separate file with the styling code in css or a javascript file, this is where you include the path to them. This will also be where you load your jsPsych library and plugins.
The head also contains the page title. This is the text that appears in the Tab when you open a webpage. Set it to “Our webpage”, open it with a browser and see what happens.
## Body
This is where we include the elements that we want to see in our webpage. Let’s start by including a text saying “Hello world!”
```
<!DOCTYPE html>
<html>
    <head>
        <title>Our webpage</title>
    </head>
    <body>
Hello world!
    </body>
</html>
```
If we save this file and open it with a browser (e.g. Chrome) we should see that the tab is named “Our webpage”, and we should see the text in our page.


# Other elements in HTML
Now, we are going to explore how to include other elements in our page. We are going to start by placing our text inside a "div". This is a container. It won’t change the appearance of our text, but it will make it easier to recall it and manipulate it later on. We will include an id (identifier) naming the div hello.
```
<!DOCTYPE html>
<html>
    <head>
        <title>Our webpage</title>
    </head>
    <body>
<div id = “hello”>Hello world!</div>
    </body>
</html>
```
If you save the document and refresh the page, you may see that, so far, nothing has changed.

Now, we are going to add a picture. For that, create a folder, inside the folder where you have your HTML file. You can name this folder whatever you would like, but it is standard to call it “img”. Drop the file of the image you would like to add in that folder.
In this case, I found the picture of a dog called George on the internet. You can find find the picture in the “img” folder inside “example_web”. 
To present the image in the wepage, we will use this line of code:

```
<!DOCTYPE html>
<html>
    <head>
        <title>Our webpage</title>
    </head>
    <body>
<div id = “hello”>Hello world!
<img id="doggy" src="img/George.png">
</div>

    </body>
</html>
```
If you refresh the page, you should now be able to see the image that you included. 
# Styling the content with css
To add style to the content, we will use css. For this, we can either create a new CSS file and link it in the head of the page, or we can include it inside our HTML file. In this case, we will use the second option. For that we will add a style tag to our page. Any content inside that tag will be read as CSS language. 

```
<!DOCTYPE html>
<html>
    <head>
        <title>Our webpage</title>
    </head>
    <body>
<div id = “hello”>Hello world!
<img id="doggy" src="img/George.png">
</div>

    </body>
<style>
</style>
</html>
```
Now we will change the font-size and position of the text and the size of the image by adding this inside our style tag:
```
#hello{
    font-size:30pt; 
    text-align:center;
}

#doggy{
    height: 200px; 
    width: 280px;
}
```
You can see that we used the “id” of the div and the image to style them. You can find documentation on how to edit different elements in css by following the links at the end of the Powerpoint presentation.
If you refresh the page now, you should see that the text and picture have both changed size. You will also observe that both the text and picture are now centred. This is because the image was included inside the “hello” div. If we move the closing tag of the div to before the picture, we will see that the text remains centred while the picture does not.
```
<!DOCTYPE html>
<html>
    <head>
        <title>Our webpage</title>
    </head>
    <body>
       <div id="hello"> Hello world!</div>
	   <img id="doggy" src="img/George.png">
    </body>
<style>
#hello{
    font-size:30pt; 
    text-align:center;
}

#doggy{
    height: 200px; 
    width: 280px;
}
	</style>
</html>
```
# Adding interactivity with JavaScript
## Basics of JavaScript
For most experiments, we need the content of a webpage to change over time and respond to participants’ actions. For that, we can use JavaScript. This language is the most similar to other programming languages, such as R or Python. It uses variables and functions. 

For example, this is how you declare a variable:
```
var x = 2
```
You can also create an array, a list of elements:

```
var y = [1, 2, 6]
```
To recall the elements from an array, you use this code, calling the first element 0, the second, 1, etc.

```
y[0]
```
Here, the outcome would be 1, which is the first element of the _y_ array.
Equally, this is how you create an object. This is another type of list in which each element is labeled.

```
var z = {
        name: "variable z",
        number: 3}
```
To recall an item from the variable z, this is what we do:

```
z.number
```
The outcome here would be 3 (the element of the object labeled number)

Let's see this in practise. If we run this:
```
var i = x + y[0] + z.number
```
The outcome would be 6, because x is 2, y[0] is 1 and z.number is 3.

Same as with CSS, if we want to include JavaScript it our webpage, we can either add a link to a separate JavaScript file in the _head_ of our wepage, or add the javaScript content inside our HTML file.

In this case, we will choose the second option. All of the content included inside the _script_ tag will be read as JavaScript.

## JavaScript in action
How can we use JavaScript in the webpage we have created so far?

First we will add a button to our page. We do this by adding the following button tag:
```
<button id = "Next" onclick="hide_dog()">Continue</button></div>
```
Here "Continue" is the text that will be displayed inside the button. Next is the identifier of the button. We have also established that when people click the button, the function named "hide_dog()" will be executed. However, we have not yet defined that function.

This function will hide the picture of the dog. To define it, we can add this within our script tags:
```
function hide_dog(){
	doggy.style.display = "none";
}
```
That way, when someone presses the "Continue" button, the dog will disappear.
This is the code so far:

```
<!DOCTYPE html>
<html>
    <head>
        <title>Our webpage</title>
    </head>
    <body>
       <div id="hello"><p>Hello world!</p><br>
	   <img id="doggy" src="img/George.png"><br>
	   <button id = "Next" onclick="hide_dog()">Continue</button></div>
    </body>
    <script>
function hide_dog(){
	doggy.style.display = "none";
}

    </script>
    <style>
#hello{
    font-size:30pt; 
    text-align:center;
}

#doggy{
    height: 200px; 
    width: 280px;
}
   </style>
</html>
```

You can also find it inside the "Example_web" folder. And those are teh basics of web programming. Now, to learn how to use this to run your jsPsych studies, go to the step-by-step tutorial for jsPsych, in the Read.me document.
