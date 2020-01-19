# PCBS_Associating_Colours

Introduction
------------


Note : in the following, a "colour" (a string refering to a colour bewteen inverted comas) refers to a word actually refering to a particular colour. On the other hand, a COLOUR refers to the colour of the font in which a word is written. For instance, BLUE "red" will refer to the word "red" written in blue.

The experiment is inspired by a well-known cognitive bias concerning fast recognition of colours. For instance, we know that a subject is slower consciously identifying a COLOUR when it is the font of another "colour" (e.g. when "red" is written in BLUE and that participants have to say "Blue") than when the COLOUR is identical to the "colour". 

The subject will face a black screen with words being displayed alternatively. The first phase will be one of learning : "colours" COLOURED in the colour they refer to will be displayed on the screen, and participants must click the right button the fastest they can.

Second, a set of chosen words will appear on screen. A third of them are "colours", another third are words clearly related to colours ("snow", "dove"... for white for example) while the final third is neutral considering colour ("abstract", "dictionary"...). Each word will be coloured in a COLOUR to which they're not related (non-congruent cases). Reaction times are measured and stored in a file. 

The idea is to compare reaction times between neutral words, "colours, and words related to colours. One point is to show if it is really the fact that a "colour" is in another COLOUR than what it refers to that slows participants in consciously recognising them, or if it's only the fact that the participant's brain has two different messages at the time (a COLOUR and a word, regardless of its connexion to colour in general). A second point is to show whether a word that is not a "colour" but only related to one can slows a participant's reaction time as strongly as a "colour".


### Organisation of the code

You'll find in this document the full code for the experiment. It mostly uses the python module expyriment.

Each different case is subset in the different blocks of the experiment, the first one being focused on the learning process, while the other three are the core of the experiment.


Experiment design and initialising
------------

### Creation of the tools

    import expyriment

    exp = expyriment.design.Experiment(name="Associating colours experiment")

    white = (255,255,255)
    black = (0,0,0)
    blue = (0,0,255)
    green = (0,255,0)

    colour_words = ["White", "Blue", "Red", "Green"]
    colour_related_words = ["Dove", "Snow", "Sea", "Sky", "Fire", "Anger", "Tree", "Nature"]
    neutral_words = ["Abstract", "Dictionary", "Losing", "Bird", "Maths", "French", "Loss", "Book"]
    colours_actual = [(255,255,255), (0,0,255), (255,0,0), (0,255,0)]

We start by importing expyriment, and launching the design phase. Here, we create the four different lists that we'll use to design our stimuli. The first three lists are all the words we'll use with actual colour nouns, colour-related words and neutral words. The last list will be used to code the font colour of the different words.

    instructions_1 = """ You will succesively see on the screen colour names, color-related nouns and colour-unrelated words. \n \n \n Each word will be in displayed in a colour font.\n\n\n Your goal is to identify the FONT COLOUR of the words as quickly as possible. \n \n \n Press the SPACE key to continue"""

    instructions_2 = """ Use the keyboard to give your answers. \n\n\n Use the keys "w" for white, "b" for blue, "r" for red and "g" for green. \n\n\n Please answer as quickly as you can.\n\n\n Press the SPACE key to continue"""
    
  In the design phase, we prepare the instructions we'll need later as well.
  
  
  ### The Blocks
  
  The experiment contains four blocks of stimuli. The first block contains all the stimuli where the COLOUR corresponds to the "colour" displayed on the screen.
  
      expyriment.control.initialize(exp)

    block_one = expyriment.design.Block(name="Learning Block")

    trial_one = expyriment.design.Trial()
    stim = expyriment.stimuli.TextLine(text=(colour_words[0]), text_colour=colours_actual[0])
    stim.preload()
    trial_one.add_stimulus(stim)

    trial_two = expyriment.design.Trial()
    stim = expyriment.stimuli.TextLine(text=(colour_words[1]), text_colour=colours_actual[1])
    stim.preload()
    trial_two.add_stimulus(stim)

    trial_three = expyriment.design.Trial()
    stim = expyriment.stimuli.TextLine(text=(colour_words[2]), text_colour=colours_actual[2])
    stim.preload()
    trial_three.add_stimulus(stim)

    trial_four = expyriment.design.Trial()
    stim = expyriment.stimuli.TextLine(text=(colour_words[3]), text_colour=colours_actual[3])
    stim.preload()
    trial_four.add_stimulus(stim)

    block_one.add_trial(trial_one)
    block_one.add_trial(trial_two)
    block_one.add_trial(trial_three)
    block_one.add_trial(trial_four)
    block_one.shuffle_trials()
    
 We create four stimuli, each of them associating a colour noun to a font colour. The order is randomised inside the block.
 
 The second block associates "colours" with non-congruent COLOURS :
 
     block_two= expyriment.design.Block(name = "Test-Colours Block")

    trial_one_two = expyriment.design.Trial()
    stim = expyriment.stimuli.TextLine(text=(colour_words[0]), text_colour=colours_actual[1])
    stim.preload()
    trial_one_two.add_stimulus(stim)

    trial_two_two = expyriment.design.Trial()
    stim = expyriment.stimuli.TextLine(text=(colour_words[1]), text_colour=colours_actual[2])
    stim.preload()
    trial_two_two.add_stimulus(stim)

    trial_three_two = expyriment.design.Trial()
    stim = expyriment.stimuli.TextLine(text=(colour_words[2]), text_colour=colours_actual[3])
    stim.preload()
    trial_three_two.add_stimulus(stim)

    trial_four_two = expyriment.design.Trial()
    stim = expyriment.stimuli.TextLine(text=(colour_words[3]), text_colour=colours_actual[0])
    stim.preload()
    trial_four_two.add_stimulus(stim)

    block_two.add_trial(trial_one_two)
    block_two.add_trial(trial_two_two)
    block_two.add_trial(trial_three_two)
    block_two.add_trial(trial_four_two)
    block_two.shuffle_trials()
    
  Block three associates colour-related words to non-congruent COLOURS :
  
      block_three= expyriment.design.Block(name="Test-Colour-Related Block")

    trial_one_three = expyriment.design.Trial()
    stim = expyriment.stimuli.TextLine(text=(colour_related_words[0]), text_colour=colours_actual[1])
    stim.preload()
    trial_one_three.add_stimulus(stim)

    trial_two_three = expyriment.design.Trial()
    stim = expyriment.stimuli.TextLine(text=(colour_related_words[1]), text_colour=colours_actual[2])
    stim.preload()
    trial_two_three.add_stimulus(stim)

    trial_three_three = expyriment.design.Trial()
    stim = expyriment.stimuli.TextLine(text=(colour_related_words[2]), text_colour=colours_actual[3])
    stim.preload()
    trial_three_three.add_stimulus(stim)

    trial_four_three = expyriment.design.Trial()
    stim = expyriment.stimuli.TextLine(text=(colour_related_words[3]), text_colour=colours_actual[0])
    stim.preload()
    trial_four_three.add_stimulus(stim)

    trial_five_three = expyriment.design.Trial()
    stim = expyriment.stimuli.TextLine(text=(colour_related_words[4]), text_colour=colours_actual[1])
    stim.preload()
    trial_five_three.add_stimulus(stim)

    trial_six_three = expyriment.design.Trial()
    stim = expyriment.stimuli.TextLine(text=(colour_related_words[5]), text_colour=colours_actual[3])
    stim.preload()
    trial_six_three.add_stimulus(stim)

    trial_seven_three = expyriment.design.Trial()
    stim = expyriment.stimuli.TextLine(text=(colour_related_words[6]), text_colour=colours_actual[0])
    stim.preload()
    trial_seven_three.add_stimulus(stim)


    trial_eight_three = expyriment.design.Trial()
    stim = expyriment.stimuli.TextLine(text=(colour_related_words[7]), text_colour=colours_actual[1])
    stim.preload()
    trial_eight_three.add_stimulus(stim)

    block_three.add_trial(trial_one_three)
    block_three.add_trial(trial_two_three)
    block_three.add_trial(trial_three_three)
    block_three.add_trial(trial_four_three)
    block_three.add_trial(trial_five_three)
    block_three.add_trial(trial_six_three)
    block_three.add_trial(trial_seven_three)
    block_three.add_trial(trial_eight_three)
    block_three.shuffle_trials()

Finally, block four associates neutral words regarding colours to random COLOURS :

    block_four = expyriment.design.Block(name="Test-Neutral Block")

    trial_one_four = expyriment.design.Trial()
    stim = expyriment.stimuli.TextLine(text=(neutral_words[0]), text_colour=colours_actual[2])
    stim.preload()
    trial_one_four.add_stimulus(stim)

    trial_two_four = expyriment.design.Trial()
    stim = expyriment.stimuli.TextLine(text=(neutral_words[1]), text_colour=colours_actual[3])
    stim.preload()
    trial_two_four.add_stimulus(stim)

    trial_three_four = expyriment.design.Trial()
    stim = expyriment.stimuli.TextLine(text=(neutral_words[2]), text_colour=colours_actual[0])
    stim.preload()
    trial_three_four.add_stimulus(stim)

    trial_four_four = expyriment.design.Trial()
    stim = expyriment.stimuli.TextLine(text=(neutral_words[3]), text_colour=colours_actual[2])
    stim.preload()
    trial_four_four.add_stimulus(stim)

    trial_five_four = expyriment.design.Trial()
    stim = expyriment.stimuli.TextLine(text=(neutral_words[4]), text_colour=colours_actual[3])
    stim.preload()
    trial_five_four.add_stimulus(stim)

    trial_six_four = expyriment.design.Trial()
    stim = expyriment.stimuli.TextLine(text=(neutral_words[5]), text_colour=colours_actual[0])
    stim.preload()
    trial_six_four.add_stimulus(stim)

    trial_seven_four = expyriment.design.Trial()
    stim = expyriment.stimuli.TextLine(text=(neutral_words[6]), text_colour=colours_actual[1])
    stim.preload()
    trial_seven_four.add_stimulus(stim)

    trial_eight_four = expyriment.design.Trial()
    stim = expyriment.stimuli.TextLine(text=(neutral_words[7]), text_colour=colours_actual[2])
    stim.preload()
    trial_eight_four.add_stimulus(stim)

    block_four.add_trial(trial_one_four)
    block_four.add_trial(trial_two_four)
    block_four.add_trial(trial_three_four)
    block_four.add_trial(trial_four_four)
    block_four.add_trial(trial_five_four)
    block_four.add_trial(trial_six_four)
    block_four.add_trial(trial_seven_four)
    block_four.add_trial(trial_eight_four)
    block_four.shuffle_trials()

(NOTE : It seems that this last block doesn't completely work on my Mac. Instead of words, there are displayed white rectangles of the pressuposed size of the words. I didn't succeed to find the cause of the problem, as I've constructed my stimuli for the fourth block like the stimuli for the other blocks.)

  ### Launching the experiment
  
Then, we add every block to the experiment, define response device from four keys ("w" for font colour "white", "b" for blue...), and launch the experiment :

    expyriment.control.start()

    instructions1.present()
    exp.keyboard.wait(expyriment.misc.constants.K_SPACE)
    instructions2.present()
    exp.keyboard.wait(expyriment.misc.constants.K_SPACE)

    for block in exp.blocks:
        for trial in block.trials:
            exp.clock.wait(1000 - trial.stimuli[0].preload())
            trial.stimuli[0].present()
            button, rt = exp.keyboard.wait(keys=response_keys)
            exp.data.add([button, rt])
            exp.data.rename("associating_colours_results" + str(exp.subject) + ".xpd")

    expyriment.control.end(goodbye_text= "Thank you !", goodbye_delay = 3000)
    
  The final line of experiment.control enable us to store the data of pressed key and response time for a potential analysis of the results. It is expected that the participants will be faster at recognising the font colour of the congruent cases of "colours" and COLOURS, as well as in the cases of neutral words. What I interstingly observed doing myself the experiment though, is that word-related colours *do* impact the response time of recognising the COLOUR (although the precise amount of this impact probably varies with the sensitivity of the participants in regards with the connexion between the colour-related word and the colour itself).
  
  Thoughts & comments
  -------------- 
  
  In the coding of this experiment, I have been confronted to difficulties that I haven't been able to solve, due to my level in programming. For instance, I haven't been able to create a function that would create the stimuli I needed, instead of creating them one by one. The fact that in blocks 2 and 3, the cases needed to be non-congruent (cases where the "colour" is not in relation with the COLOUR) was one of my main problems for that. Plus, in such configuration, a data analysis of the results is complicated, but my attempts to solve this were unsuccesful.
  As far as my level is concerned, I had never coded anything before this class. I must say that, even though the teacher and TA were there to answer questions, and although creating my own project was quite interesting, I felt a bit overwhelmed by the task. I think that the main problem is that complete beginners that might not be really comfortable with coding are in the same groups as possibly quite advanced students. As a result, even the first exercises and notions are difficult, and might be discouraging. On the other hand, this project has enabled me to find out about a very useful python module for cognitive science experiments. I'm sure that this experiment needs much improving, but it is a first step for me in the science of programming.
 
