https://pytorch.org/tutorials/beginner/Intro_to_TorchScript_tutorial.html#using-scripting-to-convert-modules

- Control Flow: loops, if statements
- pytorch derivatives: based on gradient tape
	- all operations registered to a tape
	- gradients calculated by replay them backwards through the tape
- TorchScript: 
	- provides tools to capture the model definition
	- platform "independent", can be run on many backends/devices
- **tracing**:
	- an existing Module can be traced using torch.jit.trace()
	- that captures the Module definition using TorchScript formats
	- and that in turn can be used for compiler optimisation
	- NO IF-ELSE STATEMENTS (control flows) left over when tracing:
		- run code, record operations that happen, construct ScriptModule
	- How to retain Control Flow?
		- use script compiler  torch.jit.script()
- Mixing tracing and scripting:
	- 