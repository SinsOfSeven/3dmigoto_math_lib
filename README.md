# Math Library for 3dmigoto

This is the first release of my math library for 3dmigoto.
This tool is trying to tackle some of the challenges of doing math inside of 3dmigoto mod inis.
As of now, only Cos and Rand are implemented. See [Methodology](#Methodology) for contribution guidelines.
```ini
$\math\cos\in = 40
run = commandlist\math\cos\run
x = $\math\cos\out
;x is −0.666937

$\math\rand\min = 3
$\math\rand\max = 50
run = commandlist\math\rand\run
x = $\math\rand\out
;x is [3,50]
```

## Methodology

3dmigoto inis do not have convinent functions with arguments, but we can do it by being more descriptive.
By setting the variables before we run the command, and grabbing the result after, we can get the power of functions in an ini.

We should follow this format for a consistent user experience.
- descriptive namespace bindings `$\namespace\var` and `run = commandlist\namespace\run`
- `[CommandListRun]` to envoke the primary function.
- `$out` value as the primary return.
- reset `in` inputs to appropriate values.
- Special NaN returns, when the input will never produce an output.

If your function has many inputs or outputs, you can most likely break apart your function into more generally useful parts.
You can also envoke them in eachother, which should help build a more robust toolkit.

```ini
namespace = math\function

[Constants]
;$\math\function\in
global $in
;$\math\function\out
global $out

;run = commandlist\math\function\run
[CommandListRun]
if $in != NaN
  $out = $in ** $in
else
  $out = NaN
endif
;reset $in to something appropriate.
$in = 0
```