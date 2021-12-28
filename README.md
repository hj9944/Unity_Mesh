## 第一部分：概念初析，快速理解

今天我们来唠唠Mesh这个熟悉而陌生的代名词，当然我们不是说网络模型中的Mesh，而是渲染中Mesh 网格。Mesh，俗称网格。

在计算机图形学中 ，**Mesh是指模型的网格**，我们都知道，点连成线，线连成面，面连成体，3D模型是由多边形拼接而成，而多边形实际上是由多个三角形拼接而成的，所以在三维空间中，构成这些三角形的点和边的集合就是Mesh。而通用的一些三维软件可以神奇快速生成Mesh，例如：3DMax、Maya、Cinema 4D、Blender等三维软件。针对网格的属性，建模软件的3D物体，或者程序生成的网格，网格由图形硬件（GPU Graphics Processing Unit图形处理单元）构成来绘制复杂的材料/东西。

接着，我们深度来认识**Unity中的Mesh**，我们都知道Unity是基于Mesh去做渲染的，也就是说在Unity里看见东西的话，就必须要使用Mesh，一般Unity模型的信息也会存到Mesh。Unity其实也提供一个Mesh类，允许脚本来创建和修改，通过Mesh类能生成或修改物体的网格，能做出非常酷炫的物体变形特效。其原理是：网格(Mesh)代表的是单个的可绘制实体，我们可以先来定义一个我们自己的网格类；Mesh filter 网格过滤器从资源中拿出网格并将其传递给MeshRender，用于绘制；导入模型的时候，Unity会自动创建一个这样的组件，Mesh 是网格过滤器实例化的Mesh， Mesh中存储物体的网格数据的属性和生成或修改物体网格的方法。

Unity 官方学习文档：https://docs.unity3d.com/ScriptReference/Mesh.html

Unity 官方项目库：https://github.com/Unity-Technologies/MeshSyncDCCPlugins

​	**Mesh是Unity内的一个组件，称为网格组件。**

![img](https://connect-cn-cdn-public-prd.unitychina.cn/h1/20211206/p/images/880ea8a5-e7ce-479a-9963-1f9831cfde6c_3_7.png)

**Mesh主要分为三大部分：**

- Mesh 网格
- MeshFilter 网格过滤器
- Mesh Renderer 网格渲染器

**Mesh：**是指模型的网格，建模就是建网格。细看Mesh，可以知道Mesh的主要属性内容包括顶点坐标、法线、纹理坐标、三角形绘制序列等其他有用属性和功能。因此建网格，就是画三角形；画三角形就是定位三个点。

**Mesh Filter：**内包含一个Mesh组件，可以根据MeshFilter获得模型网格的组件，也可以为MeshFilter设置Mesh内容。

**Mesh Render：**是用于把网格渲染出来的组件。MeshFilter的作用就是把Mesh扔给MeshRender将模型或者说是几何体绘制显示出来。

**Mesh的属性：**Unity中mesh主要通过Vertexs(顶点)、Normals(法线)、Triangles(三角面)、UVs(uv坐标)这四个部分数据生成。

- 顶点坐标（vertex）
- 法线（normal）
- 纹理坐标（uv）
- 三角形序列（triangle）

**顶点坐标(vertice)：**顶点坐标数组存放Mesh的每个顶点的空间坐标，假设某Mesh有n个顶点，则Vertex的size为n个。

**法线(normals)：**法线数组存放Mesh每个顶点的法线，大小与顶点坐标对应，Normal[i]对应顶点Vertex[i]的法线。

**纹理坐标(uv)：**它定义了图片上每个点的位置的信息，这些点与3D模型是相互联系的, 以决定表面纹理贴图的位置。uv是网格的基础纹理坐标，就是将图像上每一个点精确对应到模型物体的表面，uv[i]对应vertex[i] ； uv2： 网格设定的第二个纹理坐标。

**切线(tangents)：** 网格的切线数组。

**网格的包围盒(bounds)：** 网格的包围盒。

**顶点颜色(colors)：** 网格的顶点颜色数组。

**三角面(triangles)：** 包含所有三角形的顶点索引数组、vectexCount 网格中的顶点数量(只读的)、subMeshCount 子网格的数量，每个材质都有一个独立的网格列表。

**骨骼权重( bonesWeights)：** 每个顶点的骨骼权重。

**绑定姿势(bindposes)：**绑定姿势，每个索引绑定的姿势使用具有相同的索引骨骼。

**三角形序列：**每个mesh都由若干个三角形组成，而三角形的三个点就是顶点坐标里的点，三角形的数组的size = 三角形个数 * 3。

**Mesh Render：**是负责渲染的，将Mesh Filter里的Mesh通过自身的Materials渲染出来。设置完材质后，我们需要将纹理贴图与网格顶点一一对应起来，这样才能渲染出来。

**Mesh：**是指模型的网格，建模就是建网格。细看Mesh，可以知道Mesh的主要属性内容包括顶点坐标，法线，纹理坐标，三角形绘制序列等其他有用属性和功能。因此建网格，就是画三角形，画三角形就是定位三个点。

**CPU：**FBX - Meshrender （FBX通过Meshrender渲染出来）。

**FBX（模型文件）：** 包含 uv 顶点位置信息 法线 切线等渲染所需要的信息。

**MeshRender：**将这些信息 传递给GPU。

**Skin Mesh Render:** 带有蒙皮的骨骼。

**Mesh Render Mesh Filter：** Mesh Render主要将 顶点等信息传递给GPU。

**Mesh Filter：**表示将那个模型的信息传递给GPU。

**Mesh的主要优势：**

A、应用范围广泛，强大的换装游戏、Navmesh寻路系统、酷炫的游戏特效、人工智能虚拟角色赋予人性虚拟偶像、表情形变驱动等，都可以通过Mesh 实现

B、Mesh 扩展性强，无论是哪种语言，它的概念是确定的。

## 第二部分：实战应用

**实战一：基于Mesh 的基础实操。**

1、创建一个新的Mesh。

```
using UnityEngine;
public class Example : MonoBehaviour
{
    Vector3[] newVertices;
    Vector2[] newUV;
    int[] newTriangles;
   void Start()
    {
        Mesh mesh = new Mesh();
        GetComponent<MeshFilter>().mesh = mesh;
        mesh.vertices = newVertices;
        mesh.uv = newUV;
        mesh.triangles = newTriangles;
    }
}
```



2、为Mesh修改顶点属性。

```
using UnityEngine;
public class Example : MonoBehaviour
{
    void Update()
    {
        Mesh mesh = GetComponent<MeshFilter>().mesh;
        Vector3[] vertices = mesh.vertices;
        Vector3[] normals = mesh.normals;
       for (var i = 0; i < vertices.Length; I++)
        {
            vertices[i] += normals[i] * Mathf.Sin(Time.time);
        }
       mesh.vertices = vertices;
    }
}
```

3、为Mesh增加UV坐标。

uv坐标：uv坐标就是横坐标为u,纵坐标为v的一个坐标系,一般取值范围是在(0,1)之间。它代表贴图信息的位置关系,贴图每个像素点对应上的具体位置。

```
Vector2[] uvs = new Vector2[3];
uvs[0] = new Vector2(0, 0);
uvs[1] = new Vector2(0.5f, 0);
uvs[2] = new Vector2(0, 0.5f);
CurMesh.uv = uvs;
```

4、为Mesh增加法线。

法线分为顶点法线和面法线。在这个三角面上有三个顶点 和一个三角面,对应的也就有3个顶点法线和一个面法线,法线垂直于点、面，方向朝外是一个向量。

```
Vector3[] tempNormals = new Vector3[3];
tempNormals[0] = new Vector3(0, 0, -1);
tempNormals[1] = new Vector3(0, 0, -1);
tempNormals[2] = new Vector3(0, 0, -1);
CurMesh.normals = tempNormals;
```

**实战二：来自三方的实战分享**

1、Unity Mesh基础应用。

1.1 Unity Mesh基础图形的创建，从基础图形到几何体，可以参考项目中的例子： https://github.com/mattatz/unity-mesh-builder

![img](https://connect-cn-cdn-public-prd.unitychina.cn/h1/20211206/p/images/55520dbf-bb76-4a38-94eb-1047e55af78a_3_8.png)

1.2 Unity Mesh 简单创建： https://github.com/ecidevilin/UnityMeshSimplify

1.3 Mesh 切割-案例一： https://github.com/mattatz/unity-mesh-slicing

1.4 Mesh 切割-案例二： https://github.com/hugoscurti/mesh-cutter



![img](https://connect-cn-cdn-public-prd.unitychina.cn/h1/20211206/p/images/20d609f6-8cb6-4290-956b-5ee49505e76b_Square.gif)



1.5 Mesh 破裂效果: https://github.com/ElasticSea/unity-fracture

![image-20211228114441689](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20211228114441689.png)

1.6 跃动的小球： https://github.com/XJINE/Unity_OverReaction

1.7 模拟绳子效果： https://github.com/Yellowjump/unity_mesh_rope

1.8 创建Mesh 顶点图片： https://github.com/kaiware007/UnityMeshVertexTexture

1.9 Unity 官方的Mesh API： https://github.com/Unity-Technologies/MeshApiExamples

1.10 Unity框线网格生成： https://github.com/miguel12345/UnityWireframeRenderer

2、Vertex, Normal, UV Map变成立体面是基于3D图形学的原理分享。

2.1 3D Graphics: Crash Course Computer Science （基础的）：https://youtu.be/TEAtmCYYKZA

2.2 Udacity上的课程“3D Graphics” (复杂的)：https://www.udacity.com/course/interactive-3d-graphics–cs291

3、在人脸识别场景中应用。

3.1 FaceMeshBarracuda相机识别： https://github.com/keijiro/FaceMeshBarracuda

3.2 基于iPhoneX 简易版的人脸识别：

![img](https://connect-cn-cdn-public-prd.unitychina.cn/h1/20211206/p/images/cef0054e-9bea-4d64-8bbe-0e1ec0496f93_3_5.png)

A. Facial AR Remote：使用AR创作动画：https://mp.weixin.qq.com/s?__biz=MzU5MjQ1NTEwOA==&mid=2247494538&idx=1&sn=01330fa074657ffefcd9f78b476563f5&chksm=fe1ddf21c96a5637ba8d4ceb53506ff561637c39f5d7f4799a43d8e41389a4a5940d048fa087&scene=21#wechat_redirect

B. 使用Unity创建属于你自己的表情动画：https://mp.weixin.qq.com/s?__biz=MzU5MjQ1NTEwOA==&mid=2247490292&idx=1&sn=1cee65ce72ae51c3b0a6744260088739&chksm=fe1e2e5fc969a74927e64959f9f63abc47a88ca7c69ca76783408137f3a3ba9b882a075a11ba&scene=21#wechat_redirect

C. Playable API：定制你的动画系统：https://mp.weixin.qq.com/s?__biz=MzU5MjQ1NTEwOA==&mid=2247493316&idx=1&sn=7e4fef834a8066faca3d2f1f1a090bb4&chksm=fe1dd26fc96a5b79856840f556cf65026facb83520ac1891605e42d5e777d30a0d5219060e21&scene=21#wechat_redirect

所以提到 AR Face Mesh Visualizer ，它的原理是这样进行渲染脸部 (Face Rendering)：

A、当脸部数据更新时，代码会用接收到的Vertex，Normal，UV生成Mesh。

B、Face物件的Mesh Filter & Mesh Renderer 就根据最新的Mesh进行Rendering。这部分和其他物件的Rendering一样。

因此，我们能透过修改BlendShape的变量值，就能修改Mesh的形狀，这种技术常常用于面部动画(Facial Animation)中。

4、网格体素化： https://github.com/mattatz/unity-voxel

5、AR骨骼实时同步： https://github.com/jneless/wireless_AR_skeleton_realtime_sync

6、Unity Facia SDK https://github.com/Avatarchik/Unity_Facia_SDK

7、强大的布料系统。

7.1 Obi Cloth： https://assetstore.unity.com/packages/tools/physics/obi-cloth-81333

![img](https://connect-cn-cdn-public-prd.unitychina.cn/h1/20211206/p/images/05ced4f3-7b65-4070-978a-42fe1f559bd7_3_2.png)

7.2 Magic Cloth: https://assetstore.unity.com/packages/tools/physics/magica-cloth-160144

![img](https://connect-cn-cdn-public-prd.unitychina.cn/h1/20211206/p/images/b4a58a5a-2b37-459b-81cb-3042d61c534a_3_3.png)



8、跳动的文字： https://github.com/coposuke/TextMeshProAnimator

![img](https://connect-cn-cdn-public-prd.unitychina.cn/h1/20211206/p/images/ea54c3fb-69be-4e1a-be14-e9c72fb3877e_TMPA2.gif)

9、融合的皮皮球（2D）： https://github.com/dsesto/Unity-2D-Metaballs

![img](https://connect-cn-cdn-public-prd.unitychina.cn/h1/20211206/p/images/d60004eb-adce-4eff-ad2b-052b35b9def3_3_1.gif)

10、在Keijiro大神眼里， Mesh是无所不能，可以创造各种神奇酷炫的效果，如果有特别感兴趣的话，可以关注他的github 账号，里面都是满满的干货哈！

Keijiro主页：https://github.com/keijiro



![img](https://connect-cn-cdn-public-prd.unitychina.cn/h1/20211206/p/images/8d2d1989-f5f6-47c7-823f-ede3e6b6515a_3_6.png)