## How a Browser Works Internally

#### Flow 
1) Get Resources
2) Parse HTML & Create DOM Tree
	a) Consistently Changes 
3) Render Tree
4) Layout 
5) Painting 

### At the Core 

#### Executing program on Process and Thread 

After watching a rather dull, and non-detailed youtube video on the above information. I found that Google has a blog post with more details. When you start an application, it usually runs on the CPU and GPU using mechanisms provided by the OS. 

![](https://developers.google.com/web/updates/images/inside-browser/part1/CPU.png)
![](https://developers.google.com/web/updates/images/inside-browser/part1/GPU.png)
![](https://developers.google.com/web/updates/images/inside-browser/part1/hw-os-app.png)

The next important concept is Process and Thread. When you start an application a process is created. Inside of this process, you might have multiple threads to help do the work or perhaps only one. The OS will give the process a "slab" of private memory to work with. 

https://developers.google.com/web/updates/images/inside-browser/part1/memory.svg

The previously created process can also ask the OS to spin up another process to run different tasks. Different parts of memory are allocated for the new process, and the two processes can talk using Inter Process Communication.

https://developers.google.com/web/updates/images/inside-browser/part1/workerprocess.svg

#### Browser Architecture 

A web browser can be built with one process and multiple different threads, or multiple processes with a few threads. 

![](https://developers.google.com/web/updates/images/inside-browser/part1/browser-arch.png)

Note: This is not standardized, and could be approached many different ways. 

To see how many processes are running in google chrome click the three dots up top -> More Tools -> Task Manager. You can see that almost each website/tab has a dedicated process. 

![](https://developers.google.com/web/updates/images/inside-browser/part1/browserui.png)

#### The benefit of multi-process architecture in Chrome 
The advantage of having multiple processes (or one per tab) is that if a single tab has its own render process, when it becomes unresponsive you do not shut down the other processes. 

Anther benefit is security and sandboxing. Processes have their own private memory space, and often contain copies of common infrastrucure ([V8](https://v8.dev/docs)). 

You might ask yourself, well yeah, but doesnt that use more memory? It does, and apparently chrome puts a limit on how many processes it can spin up (however, my multitude of tabs open at any given time doesnt really prove this point...). This limit is set by the hardware... when it hits this limit, it will start running multiple tabs from the same site in one process. 

https://developers.google.com/web/updates/images/inside-browser/part1/tabs.svg

#### Saving more memory 
As mentioned above, the hardware can dictate the architecture of how Chrome is running. I think this is an awesome concept. When Chrome is running on *powerful* hardware it might give each service its very own process for stability. However, if you are on a device with minimal resources it will consolidate these services into one process. 

https://developers.google.com/web/updates/images/inside-browser/part1/servicfication.svg

#### Per-frame renderer processes - Site Isolation 
An important concept for this next section is cross-site iframes. Site Isolation addresses the issue of running two cross-site iframes in the same process which leads to the following vulnerabilities: 
- [Spectre](https://spectreattack.com/spectre.pdf)
- [Meltdown](https://meltdownattack.com/meltdown.pdf)

[Site isolation](https://developers.google.com/web/updates/2018/07/site-isolation) was a major engineering challenge. 


#### Up Next: Navigation 

