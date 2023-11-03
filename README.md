# JSPsych_workshop

You will find the code for the flanker task in the file experiment.html and the code for the sample webpage inside the folder "Example_webpage".

# Step-by-step instructions to create the Flanker task

## Step 1. Create a folder for your study
Create a folder for your study. Inside, create a new file and save it as HTML (Hyper Text Markup Language).

## Step 2. Get the jsPsych study template
You can obtain the template from this link (https://www.jspsych.org/7.3/tutorials/rt-task/), which is the jsPsych tutorial on creating a RT study.
Press "The complete code so far" after Step 2 of the tutorial, and you will obtain this code.


```
<!DOCTYPE html>
<html>
  <head>
    <title>My experiment</title>
    <script src="https://unpkg.com/jspsych@7.3.3"></script>
    <script src="https://unpkg.com/@jspsych/plugin-html-keyboard-response@1.1.2"></script>
    <link href="https://unpkg.com/jspsych@7.3.3/css/jspsych.css" rel="stylesheet" type="text/css" />
  </head>
  <body></body>
  <script>

    /* initialize jsPsych */
    var jsPsych = initJsPsych();

    /* create timeline */
    var timeline = [];

//THE TRIALS FOR THE STUDY WILL BE HERE
    /* define welcome message trial */
    var welcome = {
      type: jsPsychHtmlKeyboardResponse,
      stimulus: "Welcome to the experiment. Press any key to begin."
    };
    timeline.push(welcome);




//THE TRIALS FOR THE STUDY FINISH HERE
    /* start the experiment */
    jsPsych.run(timeline);

  </script>
</html>


```

