---
layout: archive
title: "Bouncing Ball"
date:
modified:
excerpt:
image:
  feature:
  teaser:
  thumb:
ads: false
---

## Dynamics

\begin{aligned}
    \frac{dx}{dt} = & v \\\\ 
    \frac{dv}{dt} = & -g - d \cdot v\\\\ 
               v' = &- k \cdot v
\end{aligned}
- - - - -

## Hybrid System Model

```drh
#define d 0.45
#define k 0.9
[0, 15] x;
[9.8] g;
[-18, 18] v;
[0, 3] time;

{ mode 1;

  invt:
        (v <= 0);
        (x >= 0);
  flow:
        d/dt[x] = v;
        d/dt[v] = -g + (- d * v ^ 1);
  jump:
        (x = 0) ==> @2 (and (x' = x) (v' = - k * v));
}
{
  mode 2;
  invt:
        (v >= 0);
        (x >= 0);
  flow:
        d/dt[x] = v;
        d/dt[v] = -g + (- d * v ^ 1);
  jump:
        (v = 0) ==> @1 (and (x' = x) (v' = v));
}
init:
@1	(and (x >= 10) (x <= 11) (v = 0));

goal:
@1	(and (x >= 0.35) (v >= -18));
```

- - - - -

## Logic Encoding

```smt2
(set-logic QF_NRA_ODE)
(declare-fun x () Real)
(declare-fun v () Real)
(declare-fun x_0_0 () Real)
(declare-fun x_0_t () Real)
(declare-fun x_1_0 () Real)
(declare-fun x_1_t () Real)
(declare-fun x_2_0 () Real)
(declare-fun x_2_t () Real)
(declare-fun x_3_0 () Real)
(declare-fun x_3_t () Real)
(declare-fun x_4_0 () Real)
(declare-fun x_4_t () Real)
(declare-fun x_5_0 () Real)
(declare-fun x_5_t () Real)
(declare-fun x_6_0 () Real)
(declare-fun x_6_t () Real)
(declare-fun x_7_0 () Real)
(declare-fun x_7_t () Real)
(declare-fun x_8_0 () Real)
(declare-fun x_8_t () Real)
(declare-fun x_9_0 () Real)
(declare-fun x_9_t () Real)
(declare-fun x_10_0 () Real)
(declare-fun x_10_t () Real)
(declare-fun v_0_0 () Real)
(declare-fun v_0_t () Real)
(declare-fun v_1_0 () Real)
(declare-fun v_1_t () Real)
(declare-fun v_2_0 () Real)
(declare-fun v_2_t () Real)
(declare-fun v_3_0 () Real)
(declare-fun v_3_t () Real)
(declare-fun v_4_0 () Real)
(declare-fun v_4_t () Real)
(declare-fun v_5_0 () Real)
(declare-fun v_5_t () Real)
(declare-fun v_6_0 () Real)
(declare-fun v_6_t () Real)
(declare-fun v_7_0 () Real)
(declare-fun v_7_t () Real)
(declare-fun v_8_0 () Real)
(declare-fun v_8_t () Real)
(declare-fun v_9_0 () Real)
(declare-fun v_9_t () Real)
(declare-fun v_10_0 () Real)
(declare-fun v_10_t () Real)
(declare-fun time_0 () Real)
(declare-fun time_1 () Real)
(declare-fun time_2 () Real)
(declare-fun time_3 () Real)
(declare-fun time_4 () Real)
(declare-fun time_5 () Real)
(declare-fun time_6 () Real)
(declare-fun time_7 () Real)
(declare-fun time_8 () Real)
(declare-fun time_9 () Real)
(declare-fun time_10 () Real)
(declare-fun mode_0 () Real)
(declare-fun mode_1 () Real)
(declare-fun mode_2 () Real)
(declare-fun mode_3 () Real)
(declare-fun mode_4 () Real)
(declare-fun mode_5 () Real)
(declare-fun mode_6 () Real)
(declare-fun mode_7 () Real)
(declare-fun mode_8 () Real)
(declare-fun mode_9 () Real)
(declare-fun mode_10 () Real)
(define-ode flow_1 ((= d/dt[x] v) (= d/dt[v] (+ (- 0.000000 9.800000) (* (- 0.000000 0.450000) (^ v 1.000000))))))
(define-ode flow_2 ((= d/dt[x] v) (= d/dt[v] (+ (- 0.000000 9.800000) (* (- 0.000000 0.450000) (^ v 1.000000))))))
(assert (<= 0.000000 x_0_0))
(assert (<= x_0_0 15.000000))
(assert (<= 0.000000 x_0_t))
(assert (<= x_0_t 15.000000))
(assert (<= 0.000000 x_1_0))
(assert (<= x_1_0 15.000000))
(assert (<= 0.000000 x_1_t))
(assert (<= x_1_t 15.000000))
(assert (<= 0.000000 x_2_0))
(assert (<= x_2_0 15.000000))
(assert (<= 0.000000 x_2_t))
(assert (<= x_2_t 15.000000))
(assert (<= 0.000000 x_3_0))
(assert (<= x_3_0 15.000000))
(assert (<= 0.000000 x_3_t))
(assert (<= x_3_t 15.000000))
(assert (<= 0.000000 x_4_0))
(assert (<= x_4_0 15.000000))
(assert (<= 0.000000 x_4_t))
(assert (<= x_4_t 15.000000))
(assert (<= 0.000000 x_5_0))
(assert (<= x_5_0 15.000000))
(assert (<= 0.000000 x_5_t))
(assert (<= x_5_t 15.000000))
(assert (<= 0.000000 x_6_0))
(assert (<= x_6_0 15.000000))
(assert (<= 0.000000 x_6_t))
(assert (<= x_6_t 15.000000))
(assert (<= 0.000000 x_7_0))
(assert (<= x_7_0 15.000000))
(assert (<= 0.000000 x_7_t))
(assert (<= x_7_t 15.000000))
(assert (<= 0.000000 x_8_0))
(assert (<= x_8_0 15.000000))
(assert (<= 0.000000 x_8_t))
(assert (<= x_8_t 15.000000))
(assert (<= 0.000000 x_9_0))
(assert (<= x_9_0 15.000000))
(assert (<= 0.000000 x_9_t))
(assert (<= x_9_t 15.000000))
(assert (<= 0.000000 x_10_0))
(assert (<= x_10_0 15.000000))
(assert (<= 0.000000 x_10_t))
(assert (<= x_10_t 15.000000))
(assert (<= -18.000000 v_0_0))
(assert (<= v_0_0 18.000000))
(assert (<= -18.000000 v_0_t))
(assert (<= v_0_t 18.000000))
(assert (<= -18.000000 v_1_0))
(assert (<= v_1_0 18.000000))
(assert (<= -18.000000 v_1_t))
(assert (<= v_1_t 18.000000))
(assert (<= -18.000000 v_2_0))
(assert (<= v_2_0 18.000000))
(assert (<= -18.000000 v_2_t))
(assert (<= v_2_t 18.000000))
(assert (<= -18.000000 v_3_0))
(assert (<= v_3_0 18.000000))
(assert (<= -18.000000 v_3_t))
(assert (<= v_3_t 18.000000))
(assert (<= -18.000000 v_4_0))
(assert (<= v_4_0 18.000000))
(assert (<= -18.000000 v_4_t))
(assert (<= v_4_t 18.000000))
(assert (<= -18.000000 v_5_0))
(assert (<= v_5_0 18.000000))
(assert (<= -18.000000 v_5_t))
(assert (<= v_5_t 18.000000))
(assert (<= -18.000000 v_6_0))
(assert (<= v_6_0 18.000000))
(assert (<= -18.000000 v_6_t))
(assert (<= v_6_t 18.000000))
(assert (<= -18.000000 v_7_0))
(assert (<= v_7_0 18.000000))
(assert (<= -18.000000 v_7_t))
(assert (<= v_7_t 18.000000))
(assert (<= -18.000000 v_8_0))
(assert (<= v_8_0 18.000000))
(assert (<= -18.000000 v_8_t))
(assert (<= v_8_t 18.000000))
(assert (<= -18.000000 v_9_0))
(assert (<= v_9_0 18.000000))
(assert (<= -18.000000 v_9_t))
(assert (<= v_9_t 18.000000))
(assert (<= -18.000000 v_10_0))
(assert (<= v_10_0 18.000000))
(assert (<= -18.000000 v_10_t))
(assert (<= v_10_t 18.000000))
(assert (<= 0.000000 time_0))
(assert (<= time_0 3.000000))
(assert (<= 0.000000 time_1))
(assert (<= time_1 3.000000))
(assert (<= 0.000000 time_2))
(assert (<= time_2 3.000000))
(assert (<= 0.000000 time_3))
(assert (<= time_3 3.000000))
(assert (<= 0.000000 time_4))
(assert (<= time_4 3.000000))
(assert (<= 0.000000 time_5))
(assert (<= time_5 3.000000))
(assert (<= 0.000000 time_6))
(assert (<= time_6 3.000000))
(assert (<= 0.000000 time_7))
(assert (<= time_7 3.000000))
(assert (<= 0.000000 time_8))
(assert (<= time_8 3.000000))
(assert (<= 0.000000 time_9))
(assert (<= time_9 3.000000))
(assert (<= 0.000000 time_10))
(assert (<= time_10 3.000000))
(assert (<= 1.000000 mode_0))
(assert (<= mode_0 2.000000))
(assert (<= 1.000000 mode_1))
(assert (<= mode_1 2.000000))
(assert (<= 1.000000 mode_2))
(assert (<= mode_2 2.000000))
(assert (<= 1.000000 mode_3))
(assert (<= mode_3 2.000000))
(assert (<= 1.000000 mode_4))
(assert (<= mode_4 2.000000))
(assert (<= 1.000000 mode_5))
(assert (<= mode_5 2.000000))
(assert (<= 1.000000 mode_6))
(assert (<= mode_6 2.000000))
(assert (<= 1.000000 mode_7))
(assert (<= mode_7 2.000000))
(assert (<= 1.000000 mode_8))
(assert (<= mode_8 2.000000))
(assert (<= 1.000000 mode_9))
(assert (<= mode_9 2.000000))
(assert (<= 1.000000 mode_10))
(assert (<= mode_10 2.000000))
(assert (and (and (= v_0_0 0.000000) (<= x_0_0 11.000000) (>= x_0_0 10.000000)) (= mode_0 1.000000) (= [x_0_t v_0_t] (integral 0. time_0 [x_0_0 v_0_0] flow_1)) (= mode_0 1.000000) (forall_t 1.000000 [0.000000 time_0] (<= v_0_t 0.000000)) (<= v_0_t 0.000000) (<= v_0_0 0.000000) (forall_t 1.000000 [0.000000 time_0] (>= x_0_t 0.000000)) (>= x_0_t 0.000000) (>= x_0_0 0.000000) (= mode_1 2.000000) (= x_0_t 0.000000) (= v_1_0 (* (- 0.000000 0.900000) v_0_t)) (= x_1_0 x_0_t) (= [x_1_t v_1_t] (integral 0. time_1 [x_1_0 v_1_0] flow_2)) (= mode_1 2.000000) (forall_t 2.000000 [0.000000 time_1] (>= v_1_t 0.000000)) (>= v_1_t 0.000000) (>= v_1_0 0.000000) (forall_t 2.000000 [0.000000 time_1] (>= x_1_t 0.000000)) (>= x_1_t 0.000000) (>= x_1_0 0.000000) (= mode_2 1.000000) (= v_1_t 0.000000) (= v_2_0 v_1_t) (= x_2_0 x_1_t) (= [x_2_t v_2_t] (integral 0. time_2 [x_2_0 v_2_0] flow_1)) (= mode_2 1.000000) (forall_t 1.000000 [0.000000 time_2] (<= v_2_t 0.000000)) (<= v_2_t 0.000000) (<= v_2_0 0.000000) (forall_t 1.000000 [0.000000 time_2] (>= x_2_t 0.000000)) (>= x_2_t 0.000000) (>= x_2_0 0.000000) (= mode_3 2.000000) (= x_2_t 0.000000) (= v_3_0 (* (- 0.000000 0.900000) v_2_t)) (= x_3_0 x_2_t) (= [x_3_t v_3_t] (integral 0. time_3 [x_3_0 v_3_0] flow_2)) (= mode_3 2.000000) (forall_t 2.000000 [0.000000 time_3] (>= v_3_t 0.000000)) (>= v_3_t 0.000000) (>= v_3_0 0.000000) (forall_t 2.000000 [0.000000 time_3] (>= x_3_t 0.000000)) (>= x_3_t 0.000000) (>= x_3_0 0.000000) (= mode_4 1.000000) (= v_3_t 0.000000) (= v_4_0 v_3_t) (= x_4_0 x_3_t) (= [x_4_t v_4_t] (integral 0. time_4 [x_4_0 v_4_0] flow_1)) (= mode_4 1.000000) (forall_t 1.000000 [0.000000 time_4] (<= v_4_t 0.000000)) (<= v_4_t 0.000000) (<= v_4_0 0.000000) (forall_t 1.000000 [0.000000 time_4] (>= x_4_t 0.000000)) (>= x_4_t 0.000000) (>= x_4_0 0.000000) (= mode_5 2.000000) (= x_4_t 0.000000) (= v_5_0 (* (- 0.000000 0.900000) v_4_t)) (= x_5_0 x_4_t) (= [x_5_t v_5_t] (integral 0. time_5 [x_5_0 v_5_0] flow_2)) (= mode_5 2.000000) (forall_t 2.000000 [0.000000 time_5] (>= v_5_t 0.000000)) (>= v_5_t 0.000000) (>= v_5_0 0.000000) (forall_t 2.000000 [0.000000 time_5] (>= x_5_t 0.000000)) (>= x_5_t 0.000000) (>= x_5_0 0.000000) (= mode_6 1.000000) (= v_5_t 0.000000) (= v_6_0 v_5_t) (= x_6_0 x_5_t) (= [x_6_t v_6_t] (integral 0. time_6 [x_6_0 v_6_0] flow_1)) (= mode_6 1.000000) (forall_t 1.000000 [0.000000 time_6] (<= v_6_t 0.000000)) (<= v_6_t 0.000000) (<= v_6_0 0.000000) (forall_t 1.000000 [0.000000 time_6] (>= x_6_t 0.000000)) (>= x_6_t 0.000000) (>= x_6_0 0.000000) (= mode_7 2.000000) (= x_6_t 0.000000) (= v_7_0 (* (- 0.000000 0.900000) v_6_t)) (= x_7_0 x_6_t) (= [x_7_t v_7_t] (integral 0. time_7 [x_7_0 v_7_0] flow_2)) (= mode_7 2.000000) (forall_t 2.000000 [0.000000 time_7] (>= v_7_t 0.000000)) (>= v_7_t 0.000000) (>= v_7_0 0.000000) (forall_t 2.000000 [0.000000 time_7] (>= x_7_t 0.000000)) (>= x_7_t 0.000000) (>= x_7_0 0.000000) (= mode_8 1.000000) (= v_7_t 0.000000) (= v_8_0 v_7_t) (= x_8_0 x_7_t) (= [x_8_t v_8_t] (integral 0. time_8 [x_8_0 v_8_0] flow_1)) (= mode_8 1.000000) (forall_t 1.000000 [0.000000 time_8] (<= v_8_t 0.000000)) (<= v_8_t 0.000000) (<= v_8_0 0.000000) (forall_t 1.000000 [0.000000 time_8] (>= x_8_t 0.000000)) (>= x_8_t 0.000000) (>= x_8_0 0.000000) (= mode_9 2.000000) (= x_8_t 0.000000) (= v_9_0 (* (- 0.000000 0.900000) v_8_t)) (= x_9_0 x_8_t) (= [x_9_t v_9_t] (integral 0. time_9 [x_9_0 v_9_0] flow_2)) (= mode_9 2.000000) (forall_t 2.000000 [0.000000 time_9] (>= v_9_t 0.000000)) (>= v_9_t 0.000000) (>= v_9_0 0.000000) (forall_t 2.000000 [0.000000 time_9] (>= x_9_t 0.000000)) (>= x_9_t 0.000000) (>= x_9_0 0.000000) (= mode_10 1.000000) (= v_9_t 0.000000) (= v_10_0 v_9_t) (= x_10_0 x_9_t) (= [x_10_t v_10_t] (integral 0. time_10 [x_10_0 v_10_0] flow_1)) (= mode_10 1.000000) (forall_t 1.000000 [0.000000 time_10] (<= v_10_t 0.000000)) (<= v_10_t 0.000000) (<= v_10_0 0.000000) (forall_t 1.000000 [0.000000 time_10] (>= x_10_t 0.000000)) (>= x_10_t 0.000000) (>= x_10_0 0.000000) (= mode_10 1.000000) (>= v_10_t -18.000000) (>= x_10_t 0.350000)))
(check-sat)
(exit)
```

## Result

<script src="/js/d3.v3.js"></script>
<script src="/js/underscore-min.js"></script>
<div id="chart-container" style="text-align:center">
<script type="text/javascript" src="/benchmarks/bouncing_ball/data.js"></script>
<script type="text/javascript" src="/js/vis.js"></script>
</div>
