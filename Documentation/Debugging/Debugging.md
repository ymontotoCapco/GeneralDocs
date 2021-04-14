# Xcode Debugging Tips



### Table of contents

1. [Introduction to Constraint Debugging](#introduction)
2. [Debugging with the lldb](#lldb)
3. [Constraint Identifiers](#identifiers)
4. [View Hierarchy Debugger](#vhd)



------



### <a name="introduction">Introduction to Constraint Debugging</a>

While programmatically creating constraints can alleviate the stress of managing constraint merge conflicts between developers, sometimes the use of Storyboards is unavoidable. When you are presented with a project that has a whole pile of constraint issues, there are some approaches that can make this step in the debugging process a little easier on you and other developers.

We will discuss the ability to debug your constraint errors right inside Xcode without having to **Run**, **Stop**, and **Run** your simulator. In general, debugging with the lldb in Xcode can be quick and effective (once you know what you want to achieve).



Let's imagine that you are working on a project and you need to adjust the `TestView.xib` of the project. After tinkering a little bit, you notice there are constraint issues and that the view no longer looks how you think it would. Now, you want to figure out why your constraints are acting up when you *know* you set the constraints correctly. There are a few ways to approach the debugging of constraints: one through the Xcode Inspector, and the other using the `lldb` inside the Xcode console.



#### <a name="lldb">Debugging with the lldb</a>

One quick and easy way is to access the object is through the `lldb`. The Lower Level Debugger allows you to execute commands on the objects and views of your choice whether through direct referencing or through manipulating the memory allocation of the view by its memory address. When dealing with constraint issues, an effective solution is to isolate the constraint by selecting the memory address (ex: `0x7fa632be08fe0`) and executing the following obj-c command in the lldb:

``` objective-c
ex [(UIView *)0x7fa632be08fe0 setBackgroundColor: [UIColor yellowColor]]
```

> ***Note***: In my opinion, this method is the quickest and easiest way to manipulate your views. It's simplicity comes from the fact that you don't have to navigate through all of your constraints to try and find the one that has ruined the view hierarchy structure.



#### <a name="identifiers">Debugging with Constraint Identifiers</a>

Another *quick* way that you can debug constraint errors is assigning an identifier to the specific constraint you want to isolate in the **Size Inspector** tab of the view in the **Interface Builder**. By doing this, we can amplify the amount of information that the debugger gives us in case of constraints errors. You will find that the Identifier will be presented in plain text in the console allowing you a quick way to identify and fix this error.
  
| <img src="https://github.com/ymontotoCapco/GeneralDocs/blob/7a8ed4765681238ff2cd797c1ee80086f8baf5e8/Documentation/Debugging/images/InterfaceBuilder.png" width="200px" /> |
| :----------------------------------------------------------: |
| <sub>Here the constraint identifier is: **\*\*first**</sub>  |



#### <a name="vhd">View Hierarchy Debugger</a>

While not as intuitive as the previous mentioned methods, there is an option to view the constraints of the view through a 3D approach. The View Hierarchy Debugger (referred to as the VHD from now on) is a tool baked into Xcode that lets you extrapolate your views into a stacked set so you can see their hierarchy structure and pinpoint the exact location, and size of the view without having to write code into the `lldb`. The VHD can simplify understanding the constraints of a view by showing them to you in an easy to digest structure in the Interface Builder right panel.

| <img src="https://github.com/ymontotoCapco/GeneralDocs/blob/7a8ed4765681238ff2cd797c1ee80086f8baf5e8/Documentation/Debugging/images/VHD.png" width="200px" /> | <img src="https://github.com/ymontotoCapco/GeneralDocs/blob/7a8ed4765681238ff2cd797c1ee80086f8baf5e8/Documentation/Debugging/images/VHD_sidebar.png" width="200px" /> |
| :----------------------------------------------------------: | :----------------------------------------------------------: |
| <sub>The View Hierarchy Debugger is the located at the bottom right above the console.</sub> | <sub>This is the description of the selected view where the frame of the view is shown.</sub> |

