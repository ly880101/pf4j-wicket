Plugin framework for Wicket
=====================

A simple plugin framework for wicket based on [PF4J] (https://github.com/decebals/pf4j). You can view wicket-plugin as a wrapper over PF4J (that is more general and can be used to create a modular Swing application for example).

Components
-------------------

- **PluginManagerInitializer** creates the plugin manager and register the created plugin manager in application using MetaDataKey.
This class load, init, start, stop and destroy plugins (using the plugin manager object). Also this class creates an PluginResourceMapper for 
each started plugin.
- **PluginResourceMapper** maps Request to PluginResourceRequestHandler and PluginResourceRequestHandler into Url (plugin/plugin-id/...).
- **PluginResourceRequestHandler** responds with a PluginResource for each request with URL like plugin/plugin-id/...
- **PluginResource** extends ResourceStreamResource and returns an UrlResourceStream (if exists a resource in plugin class loader) or a FileResourceStream.
- **PluginUtils** contains two important methods getPluginResourceUrl(PluginWrapper scope, String name) and getPluginResource(PluginWrapper scope, String name).

Using Maven
-------------------

In your pom.xml you must define the dependencies to wicket plugin artifacts with:

```xml
<dependency>
    <groupId>ro.fortsoft.wicket.plugin</groupId>
    <artifactId>wicket-plugin</artifactId>
    <version>${wicket-plugin.version}</version>
</dependency>
```

where ${wicket-plugin.version} is the last wicket plugin version.

How to use
-------------------

It's very easy to use wicket-plugin. All you need to do is to add a dependency to wicket-plugin in your pom.xml.
The main challenge for you to transform a monolithic wicket application in a modular wicket application is to identify what's your extension points and 
to write extensions for these extension point in your plugins.

For more information please see the demo sources.

Demo
-------------------

I have a tiny demo application. The demo application is in demo folder.
In demo/api folder I declared an extension point (_Section_) that is a tab in a wicket TabbedPanel.
Each section has an title, an icon and a content (a simple text message in my demo).
In demo/plugin* I implemented two plugins: plugin1, plugin2 (each plugin adds an extension for _Section_).

To run the demo application use:  
 
    ./run-demo.sh
    
In the internet browser type http://localhost:8081/.

License
--------------
  
Copyright 2012 Decebal Suiu
 
Licensed under the Apache License, Version 2.0 (the "License"); you may not use this work except in compliance with
the License. You may obtain a copy of the License in the LICENSE file, or at:
 
http://www.apache.org/licenses/LICENSE-2.0
 
Unless required by applicable law or agreed to in writing, software distributed under the License is distributed on
an "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied. See the License for the
specific language governing permissions and limitations under the License.