package me.alpha432.oyvey.features.modules.render;

import me.alpha432.oyvey.event.impl.Render3DEvent;
import me.alpha432.oyvey.event.system.Subscribe;
import me.alpha432.oyvey.features.modules.Module;
import me.alpha432.oyvey.features.settings.Setting;
import me.alpha432.oyvey.util.render.RenderUtil;
import net.minecraft.core.BlockPos;
import net.minecraft.world.level.block.entity.BarrelBlockEntity;
import net.minecraft.world.level.block.entity.ChestBlockEntity;
import net.minecraft.world.level.block.entity.ShulkerBoxBlockEntity;
import net.minecraft.world.level.block.entity.BlockEntity;
import net.minecraft.world.phys.AABB;

import java.awt.*;

public class StorageESP extends Module {

    public Setting<Color> color = color("Color", 255, 255, 0, 120);
    public Setting<Float> lineWidth = num("LineWidth", 1.5f, 0.1f, 5.0f);

    public Setting<Boolean> chests = bool("Chests", true);
    public Setting<Boolean> barrels = bool("Barrels", true);
    public Setting<Boolean> shulkers = bool("Shulkers", true);

    public StorageESP() {
        super("StorageESP", "Highlights storage blocks", Category.RENDER);
    }

    @Subscribe
    public void onRender3D(Render3DEvent event) {
        if (mc.level == null || mc.player == null) return;

        for (BlockEntity blockEntity : mc.level.blockEntityList) {

            if (blockEntity instanceof ChestBlockEntity && !chests.getValue()) continue;
            if (blockEntity instanceof BarrelBlockEntity && !barrels.getValue()) continue;
            if (blockEntity instanceof ShulkerBoxBlockEntity && !shulkers.getValue()) continue;

            if (
                blockEntity instanceof ChestBlockEntity ||
                blockEntity instanceof BarrelBlockEntity ||
                blockEntity instanceof ShulkerBoxBlockEntity
            ) {
                BlockPos pos = blockEntity.getBlockPos();
                AABB box = new AABB(
                        pos.getX(), pos.getY(), pos.getZ(),
                        pos.getX() + 1, pos.getY() + 1, pos.getZ() + 1
                );

                RenderUtil.drawBox(
                        event.getMatrix(),
                        box,
                        color.getValue(),
                        lineWidth.getValue()
                );
            }
        }
    }
}

