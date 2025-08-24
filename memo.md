
# memo

pf変化
Qが+、遅れ inductive
Qが-、進み capacitive


pf一定

Qが+、遅れ inductive
Qが-、進み capacitive

電流に対する電圧の位相を考える場合に、
位相ドリフトの電流、電圧への寄与は同じなので、
相対関係は周波数ドリフトに関係ない。


beta_p = atan((Xth*I_p+V_p*sin(theta_p))/(V_p*cos(theta_p))
beta = atan((Xth*I+V*sin(theta))/(V*cos(theta))

Eth_p = V_p*cos(theta_p)/(cos(beta_p))
Eth = V*cos(theta)/(cos(beta))

XthははじめはXth0、最初は仮定値、あとで更新
\\
V_pは1step前というか始め、
Vは1step後、
I,thetaとかも同様。
thetaは電流の値をリファレンスにした、電圧位相。
Vtheta - Itheta
位相は遅れを正にするのか、負にするのかどっちか??

## 流れ

1. increment constant kincを設定。
2. Xth0をZL0/2として設定
   ZL0 = VL0/IL0

3. (4)式
   beta = atan( (Xth*IL+VL*cos(theta))/(VL*cos(theta)))
   Eth = VL*cos(theta)/cos(beta)
   を使って

   beta, beta_preを計算。
   Eth, Eth_preを計算
4. dEth = Eth - Eth_preを計算

5. dQs=Qs_pre - Qsを計算
   
Qs_pre = Xth*_(IL_pre)^2 + QL_pre
QL_pre = VL_pre*IL_pre*sin(theta_pre)

6. dXth = Xth_pre*kinc

7. if dQs*dEth > eps:
      Xth = Xth_pre + dXth
   elif dQs*dEth < -eps:
      Xth = Xth_pre -dXth
   else:
      Xth = Xth_pre
8. update beta, Eth
   beta = atan( (Xth*IL+VL*cos(theta))/(VL*cos(theta)))
   
9. increment step, go to step3
   i = i + 1

kincの値が大きいと、収束が速いけど振動する感じか?
10回程度で収束するように、だと変化幅が大きいと時間がかかるか?

kincを動的に変えるというのはありか??

もしくは、
dXth~0になるまで、調整するものではないのか??


ref

Self-Synchronized Grid Impedance Estimation Unit Using Interpolated DFT Technique
Detection and Correction of PMU Angle Deviation for Double-Circuit Line Using Reactive Power Measurements

