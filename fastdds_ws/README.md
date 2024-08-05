## FastDDS-v2.14.2 installation

### Installtion required programs:

```
$ pip install -U colcon-common-extension vsctool
```

## Creating Workspace:

If you have your source files you can skip this part.

```
$ mkdir -p fastdds_ws/src && cd fastdds_ws
```

## Installtion repos:

If you have your source files you can skip this part.

```
$ vcs import src < fastdds-installaiton.repos
```

<br>
The example result folder structure: <br>
fastdds_ws/<br>
&ensp;└── src<br>
    &ensp;&ensp;├── fastcdr<br>
    &ensp;&ensp;├── fastdds<br>
    &ensp;&ensp;├── foonathan_memory_vendor<br>
    &ensp;&ensp;├── hello_world_example<br>
    &ensp;&ensp;├── my_package<br>
    &ensp;&ensp;└── shapes-demo<br>

## Build Packages:

### Required Packages For FastDDS (Fastcdr & Foonathan Memory):

No need to require extra arguments for build.

```
$ colcon build --packages-select fastcdr
$ colcon build --packages-select foonathan_memory_vendor
```

### FastDDS Package

Because of the version conflict of third party programs. It needs to added **Asio** need to install as outside of the program.
It needs to install version: _asio-1-30-2_ from this [Asio URL](https://github.com/chriskohlhoff/asio).
Then installtion library added to:
**fastdds_ws/fastdds/thirdparty/asio/asio/**

### Folder Structure

src/fastdds/thirdparty/<br>
&ensp;├── asio/<br>
&ensp;&ensp;│ └── asio/<br>
&ensp;&ensp;&ensp;│ ├── include/<br>
&ensp;&ensp;&ensp;│ ├── src/<br>

After adding the asio as thirdparty library we can run the build command.

```
$ colcon build --packages-select fastrtps --cmake-args -DTHIRDPARTY_Asio=FORCE -DTHIRDPARTY_UPDATE=OFF
```

Multi Thread arg: `--parallel-workers 8`
<br>
Ps: It takes _5-10_ minute for building.

### Source Application

```
$ source install/local_setup.bash
```

or

```
$ source install/setup.bash
```

Then You can check the fastdds system using _which_ command for succesfull build path control.

```
[fastdds_ws]$ which fastdds
~/Desktop/work/fastdds_ws/install/fastrtps/bin/fastdds
```

## Control The System with Hello World

Build Hello world example

```
$ colcon build --packages-select helloworld_package
```

Running as publisher & subscriber

```
$ ./build/helloworld_package/DDSHelloWorldExample publisher
```

```
$ ./build/helloworld_package/DDSHelloWorldExample subscriber
```

# Example Outputs:

<div style="-webkit-column-count: 2; -moz-column-count: 2; column-count: 2; -webkit-column-rule: 1px dotted #e0e0e0; -moz-column-rule: 1px dotted #e0e0e0; column-rule: 1px dotted #e0e0e0;">
    <div style="display: inline-block;">
        <h2>Sub</h2>
        <pre><code class="language-c">[bgokmen@dev-host-02 fastdds_ws]$ source install/setup.bash 
[bgokmen@dev-host-02 fastdds_ws]$ ./build/helloworld_package/DDSHelloWorldExample subscriber 
Starting 
Subscriber running. Please press enter to stop the Subscriber
Subscriber matched.
Message HelloWorld 1 RECEIVED
Message HelloWorld 2 RECEIVED
Message HelloWorld 3 RECEIVED
Message HelloWorld 4 RECEIVED
Message HelloWorld 5 RECEIVED
Message HelloWorld 6 RECEIVED
Message HelloWorld 7 RECEIVED
Message HelloWorld 8 RECEIVED
Message HelloWorld 9 RECEIVED
Message HelloWorld 10 RECEIVED
Subscriber unmatched.
</code></pre>
    </div>
    <div style="display: inline-block;">
        <h2>Pub</h2>
        <pre><code class="language-c">[bgokmen@dev-host-02 fastdds_ws]$ ./build/helloworld_package/DDSHelloWorldExample publisher
Starting 
Publisher running 10 samples.
Publisher matched.
Message: HelloWorld with index: 1 SENT
Message: HelloWorld with index: 2 SENT
Message: HelloWorld with index: 3 SENT
Message: HelloWorld with index: 4 SENT
Message: HelloWorld with index: 5 SENT
Message: HelloWorld with index: 6 SENT
Message: HelloWorld with index: 7 SENT
Message: HelloWorld with index: 8 SENT
Message: HelloWorld with index: 9 SENT
Message: HelloWorld with index: 10 SENT
</code></pre>
    </div>
</div>
