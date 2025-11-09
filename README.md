# VerseNoise
Verse 2D and 3D Perlin-inspired gradient noise with fractal-brownian-motion. 

## Run
Create a new noise instance. This instance encapsulates a new permutation table.
```
NoiseSampler := NewVerseNoise()
```
There are optional parameters that can be provided, here they are named with their defaults:
```
Octaves:int     = 3
Frequency:float = 0.005
Scale:float     = 1.0
Wrap:int        = 256
```
*Note: Scale is not always present in noise algorithms but I found it to be useful instead of multiplying inputs*

*Note: Wrap should be a value of the form 2^x, it generates the PermutationTable with that many elements*

### Sample
You can sample with the provided `NoiseND` functions, but this disregards octaves, frequency, and scale. You really want to take advantage of fractal-brownian-motion as it prevents noticeable tiling and banding. Not to mention, the standalone noise functions are `<decides>` so they might be a PITA for your use case.
```
SampledValue2D := FractalBrownianMotion2D(X, Y) # Where X and Y are some float values
SampledValue3D := FractalBrownianMotion3D(X, Y, Z) # ...and so is Z
```

## Performance
There is no bitwise operators in ShipVerse. This implementation must use FMod/Mod...This is not great for performance and with Verse running on 30 TPS in the BlueprintVM the runtime likes to claim infinite loop errors prematurely. Be careful out there!