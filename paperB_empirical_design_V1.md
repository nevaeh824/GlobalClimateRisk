# paper B 实证设计

## 一、实证目标

理论上，适应性投入 $$G_t$$ 一方面降低主权利差 $$s_t^g$$，另一方面通过

$$
\theta_t \equiv B_t\left(-\frac{\partial s_t^g}{\partial G_t}\right)
$$

决定 adaptation 是否足以改善下一期债务动态。当财政能力约束绑定时，若 $$\theta_t<1$$，则 economy 更接近 doom loop；若 $$\theta_t>1$$，则更接近 virtuous cycle。



因此，实证目标分为四步：

1. 估计 adaptation 对主权利差的基准半弹性。
2. 验证 adaptation 的 spread relief 是否在高债务、高气候暴露国家中更强。
4. 基于债务放大的 adaptation 边际效应构造经验上的 $$\hat\theta^{rel}_{it}$$，再用未来债务改善或未来融资条件改善检验其识别能力，并进一步寻找经验上的 regime boundary。

---

## 二、变量设计



| 变量 | 记号 | 定义 | 理论含义 |
|---|---|---|---|
| 主权利差 | $$s^g_{it}$$ | 10Y 外币主权债相对美国基准利差 | 主权融资成本 |
| 适应性指标 | $$G_{i,t-1}$$ | ND-GAIN Readiness | adaptation capacity / effective implementation ability |
| 债务率 | $$B_{i,t-1}$$ | Debt-to-GDP | 影响 $$\theta_t$$ 的核心状态变量 |
| 气候风险冲击 | $$X_{it}$$ | EM-DAT 灾害损失/GDP | 当期 physical climate shock |
| 财政紧约束 | $$Tight_{i,t-1}$$ | Interest payments / government revenue | 财政能力约束的经验代理 |
| 控制变量 | $$Z_{i,t-1}$$ | the level and growth rate of real GDP, consumer price inflation, the government budget balance as a share of GDP, international reserves as a share of GDP, and measures of institutional quality. | 主权利差标准决定因素 |



---



## 三、实证方程设计



### 3.1 回归 1：baseline spread semi-elasticity

$$
s^g_{it}
=
\alpha_i + \tau_t + \beta_1 G_{i,t-1} + \beta_2 B_{i,t-1} + \beta_3 X_{it} + \Gamma' Z_{i,t-1} + \varepsilon_{it}
$$

预期：

$$
\beta_1 < 0, \qquad \beta_2 > 0, \qquad \beta_3 > 0
$$

含义：

- adaptation 越强，主权融资成本越低；
- 债务越高，主权利差越高；
- 当期灾害损失越大，主权利差越高



### 3.2 回归 2：Corollary 1 第 1 条的验证（climate exposure 组别异质性）

paper B 的 Corollary 1 指出，adaptation 对 spread 的压缩作用，在更 climate-exposed 的经济体中更强。为避免主方程过于复杂，本文采用最简单的做法：按长期气候暴露将国家分组，再比较 $$G$$ 的系数是否更强。

实现方式有两种，正文推荐第一种。

##### 方案 A：分组回归

分别在高暴露组和低暴露组估计基准回归：

$$
s^g_{it}
=
\alpha_i + \tau_t + \beta_1^{(g)} G_{i,t-1} + \beta_2^{(g)} B_{i,t-1} + \beta_3^{(g)} X_{it} + \Gamma_g' Z_{i,t-1} + \varepsilon_{it},
\qquad g \in \{Low, High\}
$$

关注：

$$
\left|\beta_1^{(High)}\right| > \left|\beta_1^{(Low)}\right|
$$

##### 方案 B：交互项写法

$$
s^g_{it}
=
\alpha_i + \tau_t + \beta_1 G_{i,t-1} + \beta_2 B_{i,t-1} + \beta_3 X_{it} + \beta_4 \bigl(G_{i,t-1} \times HighExposure_i\bigr) + \Gamma' Z_{i,t-1} + \varepsilon_{it}
$$

预期：

$$
\beta_4 < 0
$$

由于 $$HighExposure_i$$ 是时间不变变量，在国家固定效应下其主效应会被吸收，因此只保留与 $$G$$ 的交互项即可。



### 3.3 回归 3：Corollary 1 第 2条的验证(债务放大的 adaptation 效应)

这是 paper B 中 $$\theta_t$$ 经验映射的核心方程：

$$
s^g_{it}
=
\alpha_i + \tau_t + \beta_1 G_{i,t-1} + \beta_2 B_{i,t-1} + \beta_3 \bigl(G_{i,t-1} \times B_{i,t-1}\bigr) + \beta_4 X_{it} + \Gamma' Z_{i,t-1} + \varepsilon_{it}
$$

此时，adaptation 的条件边际效应为：

$$
\frac{\partial s^g_{it}}{\partial G_{i,t-1}} = \beta_1 + \beta_3 B_{i,t-1}
$$

预期：

$$
\beta_3 < 0
$$

含义：债务越高，adaptation 对 spread 的压缩越重要。这一式直接对应 paper B 中

$$
\theta_t = B_t\left(-\frac{\partial s_t^g}{\partial G_t}\right)
$$

的经验对象。



### 3.4 回归 4：财政紧约束的更直接口径

$$
s^g_{it}
=
\alpha_i + \tau_t + \beta_1 G_{i,t-1} + \beta_2 Tight_{i,t-1} + \beta_3 \bigl(G_{i,t-1} \times Tight_{i,t-1}\bigr) + \beta_4 X_{it} + \Gamma' Z_{i,t-1} + \varepsilon_{it}
$$

这里的关键系数是：$\beta_3$

其经济含义是：在财政空间更紧时，市场对 adaptation 的定价是否更强。



### 3.5 回归 5：灾害冲击缓释效应（辅助回归）

为更直观地体现 adaptation 不是“装饰性 ESG 变量”，而是能降低 physical shock 向 financing conditions 传导的弹性，本文增加如下辅助回归：

$$
\Delta s^g_{i,t+h}
=
\alpha_{i,h} + \tau_{t,h} + \psi_h Shock_{it} + \phi_h \bigl(Shock_{it} \times G_{i,t-1}\bigr) + \Gamma_h' Z_{i,t-1} + u_{i,t+h}
$$

这里的 $$Shock_{it}$$ 可以采用major disaster dummy；

预期：

$$
\psi_h > 0, \qquad \phi_h < 0
$$

含义：在同样的灾害冲击下，高 adaptation 国家主权利差上升更小，或者回落更快。



### 3.6 经验版 $$\hat\theta^{rel}_{it}$$ 的构造与识别能力验证

先定义 spread relief 的估计值：

$$
\hat m^g_{it}
=
-
\widehat{\frac{\partial s^g_{it}}{\partial G_{i,t-1}}}
=
-
\left(\hat\beta_1 + \hat\beta_3 B_{i,t-1}\right)
$$

再定义：

$$
\hat\theta^{rel}_{it}
=
B_{i,t-1} \cdot \hat m^g_{it}
$$

定义未来债务改善：

$$
Y^B_{i,t+1}
=
-\Delta (Debt/GDP)_{i,t+1}
$$

或者未来融资条件改善：

$$
Y^s_{i,t+1}
=
-\bigl(s^g_{i,t+1}-s^g_{it}\bigr)
$$

验证回归为：

$$
Y_{i,t+1}
=
\alpha_i+\tau_t
+\delta_1 \hat\theta^{rel}_{it}
+\Gamma'Z_{it}
+u_{it}
$$

预期：

$$
\delta_1>0
$$

含义：

- $$\hat\theta^{rel}$$ 越高，未来债务动态越容易改善；
- $$\hat\theta^{rel}$$ 越高，未来 spread worsening 越弱。



进一步可做 spline：

$$
Y_{i,t+1}
=
\alpha_i+\tau_t
+\delta_1 \hat\theta^{rel}_{it}
+\delta_2(\hat\theta^{rel}_{it}-c_\theta)_+
+\Gamma'Z_{it}
+u_{it}
$$

目的：寻找经验上的 regime boundary。

还有其他方法，做到这里再看，以及绘图四象限....



