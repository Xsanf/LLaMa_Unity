This is not the final product.
The purpose of this repository is to provide a working example of using LLaMa models in Unity.
It is based on the work of https://github.com/SciSharp/LLamaSharp

It just so happened that there was a gap between the work on LLM (Large Language Models) that use Python and ordinary developers for whom such an environment is unacceptable. I would like to fill it by pushing the use of modern AI technologies in games and other applications. This example does not exhaust everything that the library provides. It allows you to load to the main LoRa model (low-rank adaptation model), quantize models and do much more. But what do you need, to good start learning?

The example iscreated as an importable Unity package.
Apologies in advance for its size, it includes the finished model wizardLM-7B.ggmlv3.q5_1.bin (https://huggingface.co/TheBloke/wizardLM-7B-GGML/tree/main)
I included the model because the example is for people who may not have the right skills to work with LLM, so they need the example to just work and allow them to learn further and realize their creativity.
In the main repository, you can see what other models you can work with and get a lot of other useful information.

What is actually done.
Unity, as a multi-platform system, lags behind the development of the NET platform, since they have to coordinate the work of all libraries.
Because of this, the example will only work on Unity 2021 and later. Earlier versions simply don't have the required level of NET support. But the master repository example still overtakes Unity and cannot be ported without fixes.

Luckily, very few fixes are needed.

1. In the main repository, the file LLamaParams.cs is replacing struct with class because memory allocation has changed.
public struct LLamaParams > public class LLamaParams

This allows you to allocate memory to it.

2. LLamaTypes.cs - Added

using System.ComponentModel;
namespace System.Runtime.CompilerServices
{
[EditorBrowsable(EditorBrowsableState.Never)]
internal static class IsExternalInit { }
}

in the NET and Unity versions, this type is not yet defined and this definition needs to be added.

Actually, that's all. Unity issues warnings, but they can be ignored. The NET documentation says that the conventions have not been changed in later versions and the panic is simply due to a formal inconsistency in the declared version.

Additionally, there is a known issue with Unity. It does not unload the .dll itself that it loaded. This leads to the impossibility of re-running the application in the development environment.

I used a quick but probably not the best solution. I look for loaded dlls through the process manager and reduce the counter of their calls there. I didn't understand why, but sometimes it doesn't help and the editor crashes.
I hope there are people who are more familiar with the problem. But this just complicates debugging, it will not affect the operation of the application.

I'll apologize right away)) I've been retired for a long time and do more with my grandchildren than programming. Therefore, I am not ready to actively participate in the development of this example.

Take it and use it, it's just an old man's attempt to push the storyline a little bit))
