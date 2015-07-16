# Mods-for-minecraft
Mods
package com.example.examplemod;

import idtech.aidan.customitem.ItemManager;
import net.minecraft.client.Minecraft;
import net.minecraft.client.renderer.entity.RenderItem;
import net.minecraft.client.resources.model.ModelResourceLocation;
import net.minecraft.init.Blocks;
import net.minecraft.init.Items;
import net.minecraft.item.Item.ToolMaterial;
import net.minecraft.item.ItemStack;
import net.minecraftforge.common.util.EnumHelper;
import net.minecraftforge.fml.common.Mod;
import net.minecraftforge.fml.common.Mod.EventHandler;
import net.minecraftforge.fml.common.event.FMLInitializationEvent;
import net.minecraftforge.fml.common.event.FMLPreInitializationEvent;
import net.minecraftforge.fml.common.registry.GameRegistry;
import net.minecraftforge.fml.relauncher.Side;

@Mod(modid = ExampleMod.MODID, version = ExampleMod.VERSION)
public class ExampleMod
{
    public static final String MODID = "examplemod";
    public static final String VERSION = "1.0";  
    public static ToolMaterial customToolMaterial;
    public static ToolMaterial customPickaxeMaterial;
    public static ToolMaterial customShovelMaterial;
    @EventHandler
    public void preinit(FMLPreInitializationEvent event){
    	customShovelMaterial = EnumHelper.addToolMaterial("CustomShovel", 1, 99999999, 100, 0, 10);
    	customToolMaterial = EnumHelper.addToolMaterial("Custom", 0, 99999999, 0, 50, 10);
    	customPickaxeMaterial = EnumHelper.addToolMaterial("CustomPickaxe", 3, 99999999, 100, 30, 10);
    	ItemManager.mainRegistry();
    	
    }
    @EventHandler
    public void init(FMLInitializationEvent event)
    {
    	GameRegistry.addShapedRecipe(new ItemStack(ItemManager.customSword),  "xy", "yx", 'x', Blocks.cobblestone, 'y', Blocks.gravel);
    	GameRegistry.addShapedRecipe(new ItemStack(ItemManager.customSword),  "yx", "yx", 'x', Blocks.cobblestone, 'y', Blocks.gravel);
    	if(event.getSide() == Side.CLIENT)
    	{
    	RenderItem renderItem= Minecraft.getMinecraft().getRenderItem();
    	renderItem.getItemModelMesher().register(ItemManager.myItem, 0, new ModelResourceLocation(this.MODID + ":" + ItemManager.myItem.name, "inventory"));
    	renderItem.getItemModelMesher().register(ItemManager.customSword, 0, new ModelResourceLocation(this.MODID + ":" + ItemManager.customSword.name, "inventory"));
    	renderItem.getItemModelMesher().register(ItemManager.customPickaxe, 0, new ModelResourceLocation(this.MODID + ":" + ItemManager.customPickaxe.name, "inventory"));
    	renderItem.getItemModelMesher().register(ItemManager.customSpade, 0, new ModelResourceLocation(this.MODID + ":" + ItemManager.customSpade.name, "inventory"));
    	}
		// some example code
        System.out.println("DIRT BLOCK >> "+Blocks.dirt.getUnlocalizedName());
    }
}
