# CNAME接入 {#concept_crt_ys2_xdb .concept}

## CNAME接入说明 {#section_wq1_zs2_xdb .section}

优势：接入方便、快速，具备智能解析和黑洞自动调度能力。

劣势：切换慢，会直接暴露游戏盾节点。

**说明：** CNAME接入只针对无法接入SDK的方式下才推荐使用，接入SDK才能享受游戏盾的完整防护能力。

## 如何获取接入CNAME？ {#section_xq1_zs2_xdb .section}

节点组的组名即为游戏盾接入调度的CNAME。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/13516/3482_zh-CN.png)

## CNAME智能调度逻辑是咋样的？ {#section_zq1_zs2_xdb .section}

默认线路： BGP线路优先级高于单线线路，如果存在BGP线路则只会透出BGP线路（最多透出2个IP），如果不存在BGP线路，则返回单线线路（最多透出6个IP）。

电信线路： 存在电信线路则优先分配，无则不分配（最多透出2个IP）

联通线路： 存在联通线路则优先分配，无则不分配（最多透出2个IP）

移动线路： 存在移动线路则优先分配，无则不分配（最多透出2个IP）

**说明：** 

-   部分节点黑洞后：自动摘除黑洞节点，自动按照以上逻辑调整DNS解析。
-   全部节点黑洞后：解析状态等同与全部节点存活。

## 如何验证智能解析效果？ {#section_ar1_zs2_xdb .section}

您可以使用 [https://www.17ce.com/](https://www.17ce.com/) 对CNAME的智能解析结果进行验证！

## 老用户会自动启用智能解析吗？ {#section_br1_zs2_xdb .section}

只有在3月21日后创建的分组才会自动启用智能解析功能，老分组需要开启调度、关闭调度、节点新增、节点删除、黑洞攻击等事件才会触发该分组的DNS解析逻辑。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/13516/3483_zh-CN.png)

