# Dialogue Summarization from a Pre-Trained Generative AI LLM Model (FLAN-T5)
---
## Table of Contents
- [Project Objective](#project-objective)
- [Tools](#tools)
- [AI Model Details](#ai-model-details)
- [DataSets](#datasets)
- [Project Steps](#project-steps)
- [Results](#results)
---
### Project Objective: To study dialogue summarization task using generative AI Pre-Trained LLM Model (FLAN-T5) and impacts of prompt engineering to achieve desired outcomes.
* We will explore the impact of input text on the output of the model
* Then we will further perform prompt engineering to attempt to achieve the desired summarization against the human labelled benchmark. 
* Next we perform zero shot, one shot, and few shot inferences and observe how it can enhance the generative output of Large Language Models like FLAN-T5 Model
---
### Tools
- `Amazon SageMaker` :  We used Amazon SageMaker and its studio to load and deploy Gen AI LLM Model for our use case with fully managed infrastructure, tools, and workflows. The Configuration details are (ml.m5.2xlarge)
- `Python`:
           We have written python code for loading the FLAN-T5 model and the test datasets from Hugging Face.
           We installed Pytorch and Hugging Face transformers and datasets modules and respective functions.
---
### AI Model Details
- Pre-trained Large Language Model(LLM) FLANT-5 from Hugging Face
- List of avialable models and documentation from Hugging Face can be referred [here](https://huggingface.co/docs/transformers/index)
___
### DataSets 
- We uploaded some simple dialogues from the [DialogSum](https://huggingface.co/datasets/knkarthick/dialogsum) Hugging Face dataset. This dataset contains 10,000+ dialogues with the corresponding human labeled summaries and topics. 
---
### Project Steps
* Step 1: We installed the required packages PyTorch and Hugging Face transformers and datasets.
* Step 2: Load the datasets, Large Language Model (LLM), tokenizer, and configurator.
* Step 3: Load the FLAN-T5 model, creating an instance of the AutoModelForSeq2SeqLM class with the .from_pretrained() method.
* Step 4: To perform encoding and decoding, you need to work with text in a tokenized form. Tokenization is the process of splitting texts into smaller units that can be processed by the LLM models.
* Step 5: Testing the tokenizer encoding and decoding a simple sentence.
* Step 6: Tokenizer is working fine its validated. Now it's time to explore how well the base LLM summarizes a dialogue without any prompt engineering. Prompt engineering is an act of a human changing the prompt (input) to improve the response for a given task.
* Step 7: Test the response of the model *without prompt engineering*<br/>
**Observation:** We see that the guesses of the model make some sense, but it doesn't seem to be sure what task it is supposed to accomplish. Seems it just makes up the next sentence in the dialogue.
* Step 8: Test the response of the model with *zero shot and few shot prompts*.<br/>
**Observation:** This is much better! But the model still does not pick up on the nuance of the conversations though.
---
### Results
* In this case, few shot did not provide much of an improvement over one shot inference.
* And, anything above 5 or 6 shot will typically not help much, either.

#### Sample Outputs of LLM
#### Zero Shot Inference
```
---------------------------------------------------------------------------------------------------
##### Example  1
---------------------------------------------------------------------------------------------------
INPUT PROMPT:

Dialogue:

#Person1#: Would you like to go to the party tonight?
#Person2#: Whose party?
#Person1#: Ruojia's. Don't you know that? Ruojia has got married.
#Person2#: What! Is she really? I can't believe it!
#Person1#: Yes. Yesterday.
#Person2#: Good gracious. That's incredible! I feel so happy for her!
#Person1#: Yes, me too.
#Person2#: But how do you know that?
#Person1#: I saw the news from her twitter. And she sent an email about it.
#Person2#: What? I didn't receive it!
#Person1#: Maybe you should check your email.
#Person2#: Oh yes, I find it. Tonight at her home. Will you bring something?
#Person1#: Yes, a pair of wineglasses and a card to wish her happy marriage.
#Person2#: I will buy a tea set.

What was going on?

---------------------------------------------------------------------------------------------------
BASELINE HUMAN SUMMARY:
#Person1# tells #Person2# that Ruojia is married and will have a party tonight. #Person2#'s surprised to know that. They will bring their gifts to bless her.

---------------------------------------------------------------------------------------------------
MODEL GENERATION - ZERO SHOT:
Ruojia got married yesterday.

---------------------------------------------------------------------------------------------------
##### Example  2
---------------------------------------------------------------------------------------------------
INPUT PROMPT:

Dialogue:

#Person1#: Taxi!
#Person2#: Where will you go, sir?
#Person1#: Friendship Hotel.
#Person2#: OK, it's not far from here.
#Person1#: I have something important to do, can you fast the speed?
#Person2#: Sure, I'll try my best. Here we are.
#Person1#: It's fast! How much should I pay you?
#Person2#: The reading on the meter is 15 yuan.
#Person1#: Here's 20 yuan, keep the change.
#Person2#: Thank you very much.

What was going on?

---------------------------------------------------------------------------------------------------
BASELINE HUMAN SUMMARY:
#Person1# takes a taxi to the Friendship Hotel for something important.

---------------------------------------------------------------------------------------------------
MODEL GENERATION - ZERO SHOT:
The taxi driver will pick up Person1 at Friendship Hotel at 20 yuan.
```
#### Few Shot Inference
```
Dialogue:

#Person1#: Would you like to go to the party tonight?
#Person2#: Whose party?
#Person1#: Ruojia's. Don't you know that? Ruojia has got married.
#Person2#: What! Is she really? I can't believe it!
#Person1#: Yes. Yesterday.
#Person2#: Good gracious. That's incredible! I feel so happy for her!
#Person1#: Yes, me too.
#Person2#: But how do you know that?
#Person1#: I saw the news from her twitter. And she sent an email about it.
#Person2#: What? I didn't receive it!
#Person1#: Maybe you should check your email.
#Person2#: Oh yes, I find it. Tonight at her home. Will you bring something?
#Person1#: Yes, a pair of wineglasses and a card to wish her happy marriage.
#Person2#: I will buy a tea set.

What was going on?
#Person1# tells #Person2# that Ruojia is married and will have a party tonight. #Person2#'s surprised to know that. They will bring their gifts to bless her.



Dialogue:

#Person1#: May, do you mind helping me prepare for the picnic?
#Person2#: Sure. Have you checked the weather report?
#Person1#: Yes. It says it will be sunny all day. No sign of rain at all. This is your father's favorite sausage. Sandwiches for you and Daniel.
#Person2#: No, thanks Mom. I'd like some toast and chicken wings.
#Person1#: Okay. Please take some fruit salad and crackers for me.
#Person2#: Done. Oh, don't forget to take napkins disposable plates, cups and picnic blanket.
#Person1#: All set. May, can you help me take all these things to the living room?
#Person2#: Yes, madam.
#Person1#: Ask Daniel to give you a hand?
#Person2#: No, mom, I can manage it by myself. His help just causes more trouble.

What was going on?
Mom asks May to help to prepare for the picnic and May agrees.



Dialogue:

#Person1#: Hello, I bought the pendant in your shop, just before. 
#Person2#: Yes. Thank you very much. 
#Person1#: Now I come back to the hotel and try to show it to my friend, the pendant is broken, I'm afraid. 
#Person2#: Oh, is it? 
#Person1#: Would you change it to a new one? 
#Person2#: Yes, certainly. You have the receipt? 
#Person1#: Yes, I do. 
#Person2#: Then would you kindly come to our shop with the receipt by 10 o'clock? We will replace it. 
#Person1#: Thank you so much. 

What was going on?
#Person1# wants to change the broken pendant in #Person2#'s shop.



Dialogue:

#Person1#: Taxi!
#Person2#: Where will you go, sir?
#Person1#: Friendship Hotel.
#Person2#: OK, it's not far from here.
#Person1#: I have something important to do, can you fast the speed?
#Person2#: Sure, I'll try my best. Here we are.
#Person1#: It's fast! How much should I pay you?
#Person2#: The reading on the meter is 15 yuan.
#Person1#: Here's 20 yuan, keep the change.
#Person2#: Thank you very much.

What was going on?

BASELINE HUMAN SUMMARY:
#Person1# takes a taxi to the Friendship Hotel for something important.

---------------------------------------------------------------------------------------------------
MODEL GENERATION - FEW SHOT:
The taxi driver will pick up Person1 at Friendship Hotel at 20 yuan.
```
---
### Limitations
* Please make sure that you do not exceed the model's input-context length which, in our case, if 512 tokens. Anything above the context length will be ignored.
---
### References
* [Amazon SageMaker](https://aws.amazon.com/sagemaker/)
* [Python 3.0](https://www.python.org/downloads/)
* [Hugging Face Models Documentation](https://huggingface.co/docs/transformers/index)
* [Dialogues DataSets](https://huggingface.co/datasets/knkarthick/dialogsum)

