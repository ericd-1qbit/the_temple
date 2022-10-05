https://pytorch.org/tutorials/beginner/Intro_to_TorchScript_tutorial.html#using-scripting-to-convert-modules

- Control Flow: loops, if statements
- pytorch derivatives: based on gradient tape
	- all operations registered to a tape
	- gradients calculated by replay them backwards through the tape
- TorchScript: provides tools to capture the model definition, platform independent
	- one aspect of it: **tracing**
	