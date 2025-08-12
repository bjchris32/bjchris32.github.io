---
layout: post
title:  "FastAI classifier project"
date:   2025-08-12
tags: [ML Learning]
img: posts/machine-learning.webp
read_time: true
show_date: true
---

This post records the journey I explored when I was following the course in [FastAI lession 2](https://course.fast.ai/Lessons/lesson2.html).

### What is drivetrain approach?
> considering your objective, then think about what actions you can take to meet that objective and what data you have (or can acquire) that can help, and then build a model that you can use to determine the best actions to take to get the best results in terms of your objective.

### How to gather data?
* At the time of writing, I used [ddgs](https://github.com/deedy5/ddgs).
The query function is as followed.
```
from ddgs import DDGS

def search_images(keywords, max_images = 200):
  results = DDGS().images(keywords, max_results = max_images)
  return L(r["image"] for r in results if "image" in r)
```

### What does Dataloader do?
* split the training and validation
* randomly select part of the image and crop it
	* because resize and padding zero will miss the key detail in the images and affect the prediction 

## What is Data Augmentation?
* creating random variations of our input data

## Training and cleaning data
* What is `model-driven data cleaning`?
> The intuitive approach to doing data cleaning is to do it /before/ you train a model. But as you’ve seen in this case, a model can actually help you find data issues more quickly and easily. So, we normally prefer to train a quick and simple model first, and then use it to help us with data cleaning.

### What animals to be classified?
I was branstorming several animal classifier as followed.
* seal v.s. sea lion v.s. sea otter
	* too hard to tell seal and sea lion by my knowledge
* otter v.s. sea otter v.s. beaver
	* too hard to tell seal and sea lion by my knowledge
* Anteater v.s. Armadillo v.s. Pangolin
	* I am able to tell the difference. So, it will be a good candidate.
* Snow Leopard v.s. Serval v.s. Leopard cat
	* I was refering to this [website](https://wuo-wuo.com/topics/widlife/64-comparison-and-similar-animals/1632-i-was-with-him-is-not-the-same-leopard-cat). But, I can not find too much result. 


## Deploy the model into an online application
* Export a model. A model consists of two parts: the `architecture` and the trained `parameters`.


### How to avoid disaster?
* Situation:
> With normal software development you can analyze the exact steps that the software is taking, and carefully study which of these steps match the desired behavior that you are trying to create. But with a neural network the behavior emerges from the model’s attempt to match the training data, rather than being exactly defined.

* Problems
	* out-of-domain data. What the model sees in production is different from what the model was trained.
	* domain-shift: the training data is not representable over time

* Solution
	* human in the loop and compare the model in parallel
	* limit the scope of the model and supervised by human
	* gradually increase the scope of the model rollout
		* aware of any significant changes 
		* think about what measure or report or picture could reflect that problem

### Unforeseen consequences
> who would be most impacted? What would the most extreme results potentially look like? How would you know what was really going on?

* We will need to construct a more careful rollout plan, with ongoing monitoring systems and human oversight

### Several trouble shooting

* `ddgs` is outdated
	* https://forums.fast.ai/t/getting-an-error-when-trying-to-run-search-images-ddg-in-google-colab/121311


* `notebook2script` is outdated and there is not such function
	* sol: https://forums.fast.ai/t/correct-export-syntax-in-nbdev-2/108043

* can not upload large files onto huggingface space
```
remote: Your push was rejected because it contains files larger than 10 MiB.
remote: Please use https://git-lfs.github.com/ to store large files.
remote: See also: https://hf.co/docs/hub/repositories-getting-started#terminal
```
	* sol: https://docs.github.com/en/repositories/working-with-files/managing-large-files/configuring-git-large-file-storage


::TODO:: combine the previoust draft post on 2025-01-09