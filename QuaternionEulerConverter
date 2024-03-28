import bpy
from mathutils import Quaternion, Euler

class QuaternionEulerVisualizerPanel(bpy.types.Panel):
    """创建一个面板在3D视图中可视化四元数与欧拉角之间的转换"""
    bl_label = "四元数与欧拉角可视化工具"
    bl_idname = "OBJECT_PT_quaternion_euler_visualizer"
    bl_space_type = 'VIEW_3D'
    bl_region_type = 'UI'
    bl_category = 'Tool'

    def draw(self, context):
        layout = self.layout
        obj = context.object

        # 当有对象被选中时显示输入字段
        if obj and (obj.type == 'MESH' or obj.type == 'ARMATURE'):
            row = layout.row()
            row.prop(obj, "rotation_mode", text="旋转模式")
            
            if obj.rotation_mode == 'QUATERNION':
                row = layout.row()
                row.prop(obj, "rotation_quaternion", text="四元数旋转")
            elif obj.rotation_mode == 'XYZ':
                row = layout.row()
                row.prop(obj, "rotation_euler", text="欧拉角旋转")
            
            row = layout.row()
            row.operator("object.convert_rotation", text="转换旋转表示")

class OBJECT_OT_ConvertRotation(bpy.types.Operator):
    """转换当前选择对象的旋转表示"""
    bl_label = "转换旋转表示"
    bl_idname = "object.convert_rotation"
    
    def execute(self, context):
        obj = context.object
        if obj.rotation_mode == 'QUATERNION':
            # 从四元数转换到欧拉角
            obj.rotation_euler = obj.rotation_quaternion.to_euler()
            obj.rotation_mode = 'XYZ'
        elif obj.rotation_mode == 'XYZ':
            # 从欧拉角转换到四元数
            obj.rotation_quaternion = obj.rotation_euler.to_quaternion()
            obj.rotation_mode = 'QUATERNION'
        return {'FINISHED'}

def register():
    bpy.utils.register_class(QuaternionEulerVisualizerPanel)
    bpy.utils.register_class(OBJECT_OT_ConvertRotation)

def unregister():
    bpy.utils.unregister_class(QuaternionEulerVisualizerPanel)
    bpy.utils.unregister_class(OBJECT_OT_ConvertRotation)

if __name__ == "__main__":
    register()
