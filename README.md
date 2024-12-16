# entity-healthbar
基岩版实体血条模板



此教程主要面向Minecraft基岩版Addon创作者，演示为自定义生物增加血条的方法，并提供创作模板。

- 常显在生物头上的，实时显示血量的血条
- 血条常亮，当血量低时改变颜色
- 血条距离摄像机超过32格则隐藏

需要使用者较熟练自定义生物的制作，blockbench的使用。详细介绍请查阅[b站专栏](https://www.bilibili.com/read/cv22115833)或docx文件。

------

# 为自定义生物增加血条

1. 增加血条粒子、贴图、动画文件，将相应文件复制到材质包的particles文件夹、textures\particle文件夹、animations文件夹即可。

2. 给实体模型增加粒子锚点，使用blockbench打开模型文件，选择合适的组，点击编辑-添加定位器（locater），即可添加一个锚点。

   拖动锚点到所需要的位置（例如实体的头顶），然后右键-重命名，将锚点的名字改为“health_bar”，保存模型。

3. 在客户端实体文件（ce文件）中定义粒子、动画。打开模板所提供的的ce文件，可以获得一些参考。

   ```json
   {
     "format_version": "1.12.0",   //注：此文件仅为ce文件编写示例
     "minecraft:client_entity": {
       "description": {
         "identifier": "nacal_sdc:your_entity",
         "particle_effects": {
           "health_bar": "nacal_sdc:health_bar" //将nacal_sdc:health_bar这个粒子的名字定义为health_bar
         },
         "animations": {
           "health_bar": "animation.health_bar" //将animation.health_bar这个动画的名字定义为health_bar
         },
         "scripts": {
           "animate": [
             "idle", //此行为示例，无需复制
             "lookat_target", //此行为示例，无需复制
             {
               "weapon": "query.is_tamed == 1" //此行为示例，无需复制
             },
             "health_bar" //将health_bar这个动画加入实体的常态播放动画，实体会重复播放此动画
           ]              //从而在“health_bar”锚点位置播放“health_bar”粒子，做到常显血条
         }
       }
     }
   }
   ```

   > 需要在自定义实体的ce文件中增加的内容有：
   >
   > 增加particle_effects以及其里面的内容（如果本身已有particle_effects则只需将"health_bar"元素加入其中）；
   >
   > 在animations加入"health_bar"元素；
   >
   > 在scripts/animate中加入"health_bar"元素。

若以上操作均准确无误，则血条已经可以正常显示。



> 参考资料：
>
> Addon制作教程-由Lintha暮辰制作：https://www.bilibili.com/video/BV1Sa411z772
>
> Blockbench教程-由酒石酸菌制作：https://www.bilibili.com/video/BV1fk4y127qg
>
> 使用Snowstorm制作粒子教程-由McHorsesMods 制作：https://www.bilibili.com/video/BV1EK411M7jV
