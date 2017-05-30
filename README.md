This project is a basic WIC codec that makes it possible to read Wow's blp files through WIC, which is very convenient since
windows explorer and default image viewer ("windows photo viewer" for windows 7, and "Photos" for win10) uses WIC.
Thus blp files can be viewed instantly in the explorer, and with the default image viewer.

Source code is not that well documented as the code itself is very simple and WIC/COM components are very well documented on the MSDN.

This is a standard COM component with some registry stuff for WIC discovery. It uses well known squish library for DXTC compression stuff.



===== About GPU stuff =====

At some point, I thought about using GPU for decompression since squish is CPU based, and DXTC is now a builtin feature in every GPU.

I made some test with cuda/dx11 shaders, but results were not that great, probably because of several factors :
- my computer is an intel i7 2600k, that is probably good enough at doing DXTC calculus which is pretty simple.
- WIC codec require the output to be in CPU memory, so data has to be copied twice, once from the memory to the GPU, then to the GPU to the memory.
- textures are not that big, mostly 512x512, not enough to have a capitalize on GPU parallelism



===== About metadata =====

WIC documentation on MSDN talks about metadata handling.
While it may be fun to have some details displayed in the explorer pane (like dxtc compression algorithm),
MSDN documentation states that for metadata handling to be actually used, the component has to be digitally signed.

Besides it seems that the default metadata viewer doesn't support display of custom properties, and I would have to 
write a custom IPropertyStore implementation, etc. 
It feels like way too much hassle for such a small change.
