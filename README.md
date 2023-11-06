# JSPsych_workshop

You will find the code for the flanker task in the file experiment.html and the code for the sample webpage inside the folder _Example_webpage_.

# Step-by-step instructions to create the Flanker task

## Step 1. Create a folder for your study
Create a folder for your study in your device. Inside the folder, create a new file and save it as HTML (Hyper Text Markup Language).

## Step 2. Get the jsPsych study template
You can obtain the template from this link (https://www.jspsych.org/7.3/tutorials/rt-task/), which is the jsPsych tutorial on creating a RT study.
Press _The complete code so far_ after Step 2 of the tutorial, and you will obtain the code below. Copy-paste this text to your html file.

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

//THE TRIALS FOR THE STUDY WILL START HERE
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
For now, your experiment has a single trial, stored under the variable _welcome_. This is html-keyboard response type of trials, which means that there will be an input written in html (e.g. formatted text) and the participant will be able to progress using their keyboard. You will be adding the new trials for your study by adding new variables in the space between the timeline creation and the start of the experiment (see comments on code above), and then pushin them to the timeline.

Now, if you open the HTML file in your browser, you should be able to see a message saying _Welcome to the experiment_. We can modify the text of the welcome trial, including, for example, the content of a participant information sheet by modifying the parameter _stimulus_. 

## Step 3. Create a consent form
After the welcome trial, we will be adding a new trial with a consent form. There are many ways to do this. Browsing through the plugins we find the _survey-multi-select_ plug in, which may be a good option for the consent form, as it allows to create a checkbox that participants will need to click to progress.

Explore the documentation of the plug in here: https://www.jspsych.org/7.3/plugins/survey-multi-select/

To _load_ this plug in, we need to copy this line of code to the "head" section of our HTML. You can find the line in the _install_ section of the plug in documentation.

```
<script src="https://unpkg.com/@jspsych/plugin-survey-multi-select@1.1.2"></script>
```
Based on the documentation and after looking at the different parameters that we can use and modify for our consent form, we are going to add this trial to the code, and then _push_ it to the timeline.

```
var consent_form = {
    type: jsPsychSurveyMultiSelect, //setting the plugin we are using
    preamble: "<p>These are the conditions of participation</p>", //inputing the text of our consent form
    questions: [
        {  
          prompt: "Do you agree?",  //inputing our questions
          options: ["Yes"],  //Including a single option to agree to the conditions of participation
          horizontal: true, //This refers to the positioning of the options in the screen, if there were more than one.
          required: true, //This makes a response from the participant a requirement to continue
          name: 'Consent'
        }
      ]
    }
timeline.push(consent_form)
```
After adding the trial and saving the changes, if we open our HTML with a browser, we should be able to see our consent form after the welcome screen.

## Step 4. Add instructions
In order to add instructions to our trial, we will again check the available plugins and select the one that works best for our case. A good option is the html-keyboard response, that allows participats to end the trial by pressing a key: https://www.jspsych.org/7.3/plugins/html-keyboard-response/

This is the same type of trial that we used for the _Welcome_, so we do NOT need to _load_ the plugin again. 

After looking through the documentation, we add this to our code:

```
  var instructions = {
      type: jsPsychHtmlKeyboardResponse,
      stimulus: "Please press the left arrow if the arrow in the centre points left and the right arrow if it points right. <br> Press any key to continue"
  }
  timeline.push(instructions)
```
## Step 5. Add a fixation cross
Now that we have a welcome screen, a consent form, and instructions, we are going to create a fixation cross for our flanker trial. Once again, a good option for this type of trial is the _html-keyboard-response_ plugin that we used for the instructions. In this case, however, we will use the parameters NOT to allow participants to end it by pressing a key, and we will set the duration to 500 ms. 

```
var cross = {
                type:jsPsychHtmlKeyboardResponse,
                stimulus: "+",
                trial_duration: 500, //Set duration to 500 ms
                choices: "NO_KEYS" //Do not allow participants to finish the trial with a key
            }
timelien.push(cross)
```
We can add this to the code. That way, participants will see a cross in the centre of the screen for half a second before proceeding to the trial.

## Step 6. Add one flanker-type trial
Now that we have a fixation cross, we are going to create our first trial of the flanker task. We first select the best plugin for our trial. Browsing through the plugins, we find the _categorize-html_ plugin. This plugin allows us to present stimuli in the screen, record a keyboard answer and provide feedback on whether the answer is correct or incorrect: https://www.jspsych.org/7.3/plugins/categorize-html/

We first _load_ the plugin by copy-pasting this line of code into our _head_ section. This can be found in the _Install_ section of the plugin documentation:

```
<script src="https://unpkg.com/@jspsych/plugin-categorize-html@1.1.2"></script>
```
We identify the name the correct name of the keys that we are going to allow in our trial, the left and right arrows: https://developer.mozilla.org/en-US/docs/Web/API/UI_Events/Keyboard_event_key_values
This link can be found in the "choices" section of any of the plugins involving keyboard responses.
Then, based on the available parameters, we add this trial to our code and _push_ it to the timeline:

```

var flanker = {
    type: jsPsychCategorizeHtml,
    stimulus: ">>>>>"
    key_answer: "ArrowRight"
    correct_text: "Correct!",
    incorrect_text: "Incorrect",
    choices: ["ArrowRight", "ArrowLeft"],
    trial_duration: 2000
}

timeline.push(flanker)

```

Now, if we open our HTML file in a browser, we should be able to see the welcome screen, the consent form, the instructions, and then a flanker-type trial with a duration of two seconds, that gives us feedback on our selection.

## Step 7. Use timeline-variables to create more flanker-type trials
We could create the rest of our flanker trials by adding them manually, like in the example above. But this would not allow us to do things such as randomising the order of presentation, and it is not the most efficient way to do it. For that reason, we will use timeline variables. There is extensive documentation on how to use timeline variables in the "Creating an Experiment" section of the jsPsych documentation: https://www.jspsych.org/7.3/overview/timeline/

Based on that, we first identify the trials of our study that need to be repeated. These are the fixation cross and the flanker trial. We can merge these into a single trial by creating a timeline variable within our flanker trial. Next, we use timeline variables to modify the content of the flanker trial in each ocassion (i.e. the direction the centre arrow is pointing to and whether it is congruent or incongrount), like in the code below:

```

    var flanker = {
        timeline : [
            {
                type:jsPsychHtmlKeyboardResponse,
                stimulus: "+",
                trial_duration: 500,
                choices: "NO_KEYS"
            },
            {
        type: jsPsychCategorizeHtml,
        stimulus: jsPsych.timelineVariable('stimulus'),
        key_answer: jsPsych.timelineVariable('key_answer'),
        correct_text: "Correct!",
        incorrect_text: "Incorrect",
        choices: ["ArrowRight", "ArrowLeft"],
		    trial_duration: 2000
            } 
        ],
        timeline_variables : [
            {stimulus: "<<<<<", key_answer: "ArrowLeft"},
            {stimulus: "<<><<", key_answer: "ArrowRight"},
            {stimulus: ">>>>>", key_answer: "ArrowRight"},
            {stimulus: ">><>>", key_answer: "ArrowLeft"}
        ],
        randomize_order: true

    }
    timeline.push(flanker)
```

We also randomised the order of presentation of the trials. If we wanted to manipulate the number of trials, we could use further timeline parameters. A further development of these can be found in the timeline documentation: https://www.jspsych.org/7.3/overview/timeline/

## Step 8: Test that it works
We have now created a simple flanker task study. We can now test that it works by running the html in our browser. If it is not running properly, we can open the console by pressing "Control + Shift + i" in our browser or searching for the _Developer mode_ option. There should be an error message indicating the code line in which the issue is.

JavaScript is case-sensitive, but not indentation sensitive. The most common problems are:
- Brackets {} or [] have not been closed or are closed in the wrong location
- There is a comma missing between the elements inside an object {} or array []
- The spelling of a variable is incorrect (e.g. writing _answer_key_ instead of _key_answer_, writing _jsPsych.TimelineVariable_ instead of _jsPsych.timelineVariable_, or referring to a variable in two different ways in different parts of the code).
- The quotes have been misused. You should use quotes (single quotes or double quotes are equivalent) to add text to your study. For exmaple, in the stimuli section of your variables or when indicating a key. The quotes make it a _string_ variable. You can find in the description of the plugins which parameters should be _strings_. If you use a string where you shouldn't and viceversa, the experiment will not work.

And that's it! You can find the full finished code in the file experiment.html

