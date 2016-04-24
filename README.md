# Minecraft Modding

## Setup
1) Download **forge source/development kit 1.8 mdk** from
http://files.minecraftforge.net

  ```
  unzip forge-1.8-11.14.4.1577-mdk.zip forge-1.8
  ```

2) Set up a forge workspace for eclipse

  ```
  cd forge-1.8
  ./gradlew setupDecompWorkspace eclipse
  ```

3) Launch eclipse and open the project in **forge-1.8/eclipse** directory

4) Run the Client

5) Verify that Minecraft is up and running.

## Creating the first Mod

1) In Eclipse, right-click **src/main/java** folder, and create a new package, e.g., **learning.forge.mods**

2) Under **learning.forge.mods** package, create a new class in **Main.java**

```java
package learning.forge.mods;

import net.minecraftforge.common.MinecraftForge;
import net.minecraftforge.fml.common.Mod;
import net.minecraftforge.fml.common.Mod.EventHandler;
import net.minecraftforge.fml.common.event.FMLInitializationEvent;

@Mod(modid = Main.MODID, version = Main.VERSION)
public class Main {
	public static final String MODID = "learningMods";
	public static final String VERSION = "1.0";

	@EventHandler
	public void init(FMLInitializationEvent event) {
	}
}
```

3) Adding the Event Handler class in **BlockBreakMessage.java**

```java
package learning.forge.mods;

import net.minecraft.util.ChatComponentText;
import net.minecraft.util.EnumChatFormatting;
import net.minecraftforge.event.world.BlockEvent.BreakEvent;
import net.minecraftforge.fml.common.eventhandler.SubscribeEvent;

public class BlockBreakMessage {

	@SubscribeEvent
	public void sendMessage(BreakEvent event) {
		event.getPlayer()
			.addChatComponentMessage(new ChatComponentText(EnumChatFormatting.GOLD + "You broke a block!"));
	}
}
```

4) Registering the Event Handler on the Event Bus in **Main.java**

```java
package learning.forge.mods;

import net.minecraftforge.common.MinecraftForge;
import net.minecraftforge.fml.common.Mod;
import net.minecraftforge.fml.common.Mod.EventHandler;
import net.minecraftforge.fml.common.event.FMLInitializationEvent;

@Mod(modid = Main.MODID, version = Main.VERSION)
public class Main {
	public static final String MODID = "learningMods";
	public static final String VERSION = "1.0";

	@EventHandler
	public void init(FMLInitializationEvent event) {
		MinecraftForge.EVENT_BUS.register(new BlockBreakMessage());		
	}

}
```

5) Running Minecraft and Verifying the Mod
  - In Eclipse, launch the client.
  - In Minecraft, create a **New World** in **Creative** mode.
  - In the Minecraft world, try to break a block.
  - You should get a message like **"You broke a block!"**

## Mod example codes from the "Minecraft Modding with Forge" book:
  https://github.com/AdityaGupta1/minecraft-modding-book/tree/master/src/main/java/org/devoxx4kids/forge/mods

## Issues and Solutions

- When running **./gradlew setupDecompWorkspace eclipse**:
  - Issue: *OBJModel.java:617: error: cannot find symbol*

  > Solution:
    - Download [vecmath-1.5.2.jar](https://github.com/cltran2/minecraft-modding/blob/master/vecmath-1.5.2.jar?raw=true) (originally from http://www.java2s.com/Code/Jar/v/Downloadvecmathjar.htm)
    - Place it in **/Library/Java/Extensions/** so that it takes precedence over the OS X version provided in /System/Library/Java/Extensions/
    ```
    sudo cp vecmath-1.5.2.jar /Library/Java/Extensions/vecmath.jar
    ```
    - For more details, see https://github.com/MinecraftForge/MinecraftForge/issues/2183#issuecomment-156540131

+ When run the Client in Eclipse:
  - Issue: *Variable references empty selection: ${project_loc}*

  > Solution: in Package Explorer, select **MDKExample > src/main/java**
