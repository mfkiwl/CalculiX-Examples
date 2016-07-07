# Eye/Pin Contact 2D
Tested with CGX/CCX 2.10

+ Plane strain model
+ Linear elastic pin, elasto-plastic eye
+ Node-to-surface Penalty contact
+ Prescribed displacement of the pin

The model was inspired by a  [model ](https://groups.yahoo.com/neo/groups/calculix/files/examples/eyebar%20with%20contact%20and%20nonlinear%20material/) by user dichtstoff in the CalculiX user forum. Here, essentially, parametrization with the script `param.py` was added.


| File                   | Contents                                      |
| :-------------         | :-------------                                |
| [par.eyebar.fbd](par.eyebar.fbd)     | Pre-processing script for CGX  (parametrized with `param.py`)                |
| [eyebar.inp](eyebar.inp) | CCX input |
| [post.fbd](post.fbd)   | CGX post-processing script                    |
| [df.gnu](df.gnu)   | Gnuplot script for the force-displacement plot    |


## Preprocessing
Two separate parts are generated and meshed with plane strain elements.
The prescribed displacement is applied to the flat equatorial surface of the pin.

```
> param.py par.eyebar.fbd
> cgx -b eyebar.fbd
```
<img src="mesh.png">

## Solving
```
> ccx eyebar
> monitor.py eyebar
```
<img src="eyebar.png" title="Convergence plot">

## Postprocess

```
> cgx -b post.fbd
```
<img src="SE.png" width="400" title="Equivalent stress">
<img src="PE.png" width="400" title="Equivalent plastic strain">

The force-displacement curve is valid for the half model and is created from the .dat-file-output
of the total reaction forces and the displacement of the monitor node.

<img src="df.png" width="400" title="Force-displacement curve">