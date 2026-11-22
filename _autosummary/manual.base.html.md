# manual.base

Base objects

### Functions

| [`mk_command_runner`](#manual.base.mk_command_runner)(commands_template[, name, ...])   | Make a python function from a sequence of templated system commands.   |
|------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------|

### manual.base.mk_command_runner(commands_template, name=None, , step_by_step=False)

Make a python function from a sequence of templated system commands.

* **Parameters:**
  * **commands_template** – Multi-line string of commands or list of commands
  * **name** – The name we want the output function to be called
  * **step_by_step** – Set to True if we want the commands to be run one by one

```pycon
>>> mytest = mk_command_runner([
...     'export {env_var}="{value}"',
...     'echo {env_var}',
...     'unset {env_var}',
... ])
>>> from inspect import signature
>>> str(signature(mytest))
'(env_var, value, *, _dry_run=False)'
>>> mytest('__SOME_ENV_VAR_FOR_TESTING__', 'test 123')

(1/3)$ export __SOME_ENV_VAR_FOR_TESTING__="test 123"

(2/3)$ echo __SOME_ENV_VAR_FOR_TESTING__
__SOME_ENV_VAR_FOR_TESTING__


(3/3)$ unset __SOME_ENV_VAR_FOR_TESTING__
```
