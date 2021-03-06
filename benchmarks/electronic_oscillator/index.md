---
layout: archive
title: "Electronic Oscillator Model"
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

The EO model represents an electronic oscillator model that contains nonlinear ODEs such as the following:
\begin{aligned}
\frac{dx}{dt}       =& - ax \cdot sin(\omega_1 \cdot \tau) \\\\ 
\frac{dy}{dt}       =& - ay \cdot sin( (\omega_1 + c_1) \cdot \tau) \cdot sin(\omega_2)\cdot 2 \\\\ 
\frac{dz}{dt}       =& - az \cdot sin( (\omega_2 + c_2) \cdot \tau) \cdot cos(\omega_1)\cdot 2 \\\\ 
\frac{\omega_1}{dt} =& - c_3\cdot \omega_1 \\\\ 
\frac{\omega_2}{dt} =& - c_4\cdot\omega_2 \\\\ 
\frac{d\tau}{dt}    =& 1
\end{aligned}

- - - - -

## Hybrid System Model

```drh
#define omega 3.14

#define ax 1
#define ay 1.2
#define az 0.8

[-5, 5] x;
[-5, 5] y;
[-5, 5] z;

[-4, 4] omega1;
[-4, 4] omega2;

[0, 200] tau;
[0, 200] time;

{mode 1;

invt:
        (x >= -5);
        (y >= -5);
        (z >= -5);
        (omega1 >= -3.14);
        (omega2 >= -3.14);
        (tau <= 5);

flow:
        d/dt[x] = - ax * sin(omega * tau);
        d/dt[y] = - ay * sin( (omega1 + 1.0) * tau) * sin(omega2)*2;
        d/dt[z] = - az * sin( (omega2 + 1.0) * tau) * cos(omega1)*2;
        d/dt[omega1] = ( 0 - 0.5 * omega1);
        d/dt[omega2] = ( 0 - omega2);
        d/dt[tau] = 1;

jump: (and (tau >= 4)) ==> @2 ( and (tau' = 0) (x' = x) (y' = y * 0.2) (z' = z) (omega1' = 1.5) (omega2' = 1));

}

{mode 2;

invt:
        (x >= -5);
        (y >= -5);
        (z >= -5);
        (omega1 >= -3.14);
        (omega2 >= -3.14);
        (tau <= 10);

flow:
        d/dt[x] = - ax * sin(omega * tau);
        d/dt[y] = - ay * sin( (omega1 + 1.0) * tau) * sin(omega2)*2;
        d/dt[z] = - az * sin( (2.0 - omega2) * tau) * sin(omega1)*2;
        d/dt[omega1] = (0 - omega1);
        d/dt[omega2] = ( 0 - omega2);
        d/dt[tau] = 1;

jump: (and (tau >= 8)) ==> @3 (and (tau' = 0) (x' = 0.2 * x) (y' = y * 0.5 ) (z' = z) (omega1' = sin(omega1)) (omega2' = (0- omega2)));
}


{mode 3;

invt:
        (x >= -5);
        (y >= -5);
        (z >= -5);
        (omega1 >= -3.14);
        (omega2 >= -3.14);
        (tau <= 6);

flow:
        d/dt[x] = - ax * sin(omega * tau);
        d/dt[y] = - ay * sin( (omega1 + 1.0) * tau) * sin(omega2)*2;
        d/dt[z] = - az * sin( (omega2 + 2.0) * tau) * cos(omega1)*2;
        d/dt[omega1] = ( 0 - 0.5 * omega1);
        d/dt[omega2] = ( 0 - omega2);
        d/dt[tau] = 1;

jump: (and (tau >= 5)) ==> @1 ( and (tau' = 0) (x' = x) (y' = y) (z' = z) (omega1' = 1) (omega2' = 1));

}


init:
@1 (and (x <= 0.1) (x >= - 0.2) (y = 0) (z = 0) (tau = 0) (omega1 = 2) (omega2 = 2.5));

goal:
@3 (tau = 4.0);
```

- - - - -

## Logic Encoding

```smt2
(set-logic QF_NRA_ODE)
(declare-fun z () Real)
(declare-fun y () Real)
(declare-fun x () Real)
(declare-fun tau () Real)
(declare-fun omega2 () Real)
(declare-fun omega1 () Real)
(declare-fun z_0_0 () Real)
(declare-fun z_0_t () Real)
(declare-fun z_1_0 () Real)
(declare-fun z_1_t () Real)
(declare-fun z_2_0 () Real)
(declare-fun z_2_t () Real)
(declare-fun z_3_0 () Real)
(declare-fun z_3_t () Real)
(declare-fun z_4_0 () Real)
(declare-fun z_4_t () Real)
(declare-fun z_5_0 () Real)
(declare-fun z_5_t () Real)
(declare-fun y_0_0 () Real)
(declare-fun y_0_t () Real)
(declare-fun y_1_0 () Real)
(declare-fun y_1_t () Real)
(declare-fun y_2_0 () Real)
(declare-fun y_2_t () Real)
(declare-fun y_3_0 () Real)
(declare-fun y_3_t () Real)
(declare-fun y_4_0 () Real)
(declare-fun y_4_t () Real)
(declare-fun y_5_0 () Real)
(declare-fun y_5_t () Real)
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
(declare-fun tau_0_0 () Real)
(declare-fun tau_0_t () Real)
(declare-fun tau_1_0 () Real)
(declare-fun tau_1_t () Real)
(declare-fun tau_2_0 () Real)
(declare-fun tau_2_t () Real)
(declare-fun tau_3_0 () Real)
(declare-fun tau_3_t () Real)
(declare-fun tau_4_0 () Real)
(declare-fun tau_4_t () Real)
(declare-fun tau_5_0 () Real)
(declare-fun tau_5_t () Real)
(declare-fun omega2_0_0 () Real)
(declare-fun omega2_0_t () Real)
(declare-fun omega2_1_0 () Real)
(declare-fun omega2_1_t () Real)
(declare-fun omega2_2_0 () Real)
(declare-fun omega2_2_t () Real)
(declare-fun omega2_3_0 () Real)
(declare-fun omega2_3_t () Real)
(declare-fun omega2_4_0 () Real)
(declare-fun omega2_4_t () Real)
(declare-fun omega2_5_0 () Real)
(declare-fun omega2_5_t () Real)
(declare-fun omega1_0_0 () Real)
(declare-fun omega1_0_t () Real)
(declare-fun omega1_1_0 () Real)
(declare-fun omega1_1_t () Real)
(declare-fun omega1_2_0 () Real)
(declare-fun omega1_2_t () Real)
(declare-fun omega1_3_0 () Real)
(declare-fun omega1_3_t () Real)
(declare-fun omega1_4_0 () Real)
(declare-fun omega1_4_t () Real)
(declare-fun omega1_5_0 () Real)
(declare-fun omega1_5_t () Real)
(declare-fun time_0 () Real)
(declare-fun time_1 () Real)
(declare-fun time_2 () Real)
(declare-fun time_3 () Real)
(declare-fun time_4 () Real)
(declare-fun time_5 () Real)
(declare-fun mode_0 () Real)
(declare-fun mode_1 () Real)
(declare-fun mode_2 () Real)
(declare-fun mode_3 () Real)
(declare-fun mode_4 () Real)
(declare-fun mode_5 () Real)
(define-ode flow_1 ((= d/dt[x] (* -1.000000 (sin (* 3.140000 tau)))) (= d/dt[y] (* (* (* -1.200000 (sin (* (+ omega1 1.000000) tau))) (sin omega2)) 2.000000)) (= d/dt[z] (* (* (* -0.800000 (sin (* (+ omega2 1.000000) tau))) (cos omega1)) 2.000000)) (= d/dt[omega1] (- 0.000000 (* 0.500000 omega1))) (= d/dt[omega2] (- 0.000000 omega2)) (= d/dt[tau] 1.000000)))
(define-ode flow_2 ((= d/dt[x] (* -1.000000 (sin (* 3.140000 tau)))) (= d/dt[y] (* (* (* -1.200000 (sin (* (+ omega1 1.000000) tau))) (sin omega2)) 2.000000)) (= d/dt[z] (* (* (* -0.800000 (sin (* (- 2.000000 omega2) tau))) (sin omega1)) 2.000000)) (= d/dt[omega1] (- 0.000000 omega1)) (= d/dt[omega2] (- 0.000000 omega2)) (= d/dt[tau] 1.000000)))
(define-ode flow_3 ((= d/dt[x] (* -1.000000 (sin (* 3.140000 tau)))) (= d/dt[y] (* (* (* -1.200000 (sin (* (+ omega1 1.000000) tau))) (sin omega2)) 2.000000)) (= d/dt[z] (* (* (* -0.800000 (sin (* (+ omega2 2.000000) tau))) (cos omega1)) 2.000000)) (= d/dt[omega1] (- 0.000000 (* 0.500000 omega1))) (= d/dt[omega2] (- 0.000000 omega2)) (= d/dt[tau] 1.000000)))
(assert (<= -5.000000 z_0_0))
(assert (<= z_0_0 5.000000))
(assert (<= -5.000000 z_0_t))
(assert (<= z_0_t 5.000000))
(assert (<= -5.000000 z_1_0))
(assert (<= z_1_0 5.000000))
(assert (<= -5.000000 z_1_t))
(assert (<= z_1_t 5.000000))
(assert (<= -5.000000 z_2_0))
(assert (<= z_2_0 5.000000))
(assert (<= -5.000000 z_2_t))
(assert (<= z_2_t 5.000000))
(assert (<= -5.000000 z_3_0))
(assert (<= z_3_0 5.000000))
(assert (<= -5.000000 z_3_t))
(assert (<= z_3_t 5.000000))
(assert (<= -5.000000 z_4_0))
(assert (<= z_4_0 5.000000))
(assert (<= -5.000000 z_4_t))
(assert (<= z_4_t 5.000000))
(assert (<= -5.000000 z_5_0))
(assert (<= z_5_0 5.000000))
(assert (<= -5.000000 z_5_t))
(assert (<= z_5_t 5.000000))
(assert (<= -5.000000 y_0_0))
(assert (<= y_0_0 5.000000))
(assert (<= -5.000000 y_0_t))
(assert (<= y_0_t 5.000000))
(assert (<= -5.000000 y_1_0))
(assert (<= y_1_0 5.000000))
(assert (<= -5.000000 y_1_t))
(assert (<= y_1_t 5.000000))
(assert (<= -5.000000 y_2_0))
(assert (<= y_2_0 5.000000))
(assert (<= -5.000000 y_2_t))
(assert (<= y_2_t 5.000000))
(assert (<= -5.000000 y_3_0))
(assert (<= y_3_0 5.000000))
(assert (<= -5.000000 y_3_t))
(assert (<= y_3_t 5.000000))
(assert (<= -5.000000 y_4_0))
(assert (<= y_4_0 5.000000))
(assert (<= -5.000000 y_4_t))
(assert (<= y_4_t 5.000000))
(assert (<= -5.000000 y_5_0))
(assert (<= y_5_0 5.000000))
(assert (<= -5.000000 y_5_t))
(assert (<= y_5_t 5.000000))
(assert (<= -5.000000 x_0_0))
(assert (<= x_0_0 5.000000))
(assert (<= -5.000000 x_0_t))
(assert (<= x_0_t 5.000000))
(assert (<= -5.000000 x_1_0))
(assert (<= x_1_0 5.000000))
(assert (<= -5.000000 x_1_t))
(assert (<= x_1_t 5.000000))
(assert (<= -5.000000 x_2_0))
(assert (<= x_2_0 5.000000))
(assert (<= -5.000000 x_2_t))
(assert (<= x_2_t 5.000000))
(assert (<= -5.000000 x_3_0))
(assert (<= x_3_0 5.000000))
(assert (<= -5.000000 x_3_t))
(assert (<= x_3_t 5.000000))
(assert (<= -5.000000 x_4_0))
(assert (<= x_4_0 5.000000))
(assert (<= -5.000000 x_4_t))
(assert (<= x_4_t 5.000000))
(assert (<= -5.000000 x_5_0))
(assert (<= x_5_0 5.000000))
(assert (<= -5.000000 x_5_t))
(assert (<= x_5_t 5.000000))
(assert (<= 0.000000 tau_0_0))
(assert (<= tau_0_0 200.000000))
(assert (<= 0.000000 tau_0_t))
(assert (<= tau_0_t 200.000000))
(assert (<= 0.000000 tau_1_0))
(assert (<= tau_1_0 200.000000))
(assert (<= 0.000000 tau_1_t))
(assert (<= tau_1_t 200.000000))
(assert (<= 0.000000 tau_2_0))
(assert (<= tau_2_0 200.000000))
(assert (<= 0.000000 tau_2_t))
(assert (<= tau_2_t 200.000000))
(assert (<= 0.000000 tau_3_0))
(assert (<= tau_3_0 200.000000))
(assert (<= 0.000000 tau_3_t))
(assert (<= tau_3_t 200.000000))
(assert (<= 0.000000 tau_4_0))
(assert (<= tau_4_0 200.000000))
(assert (<= 0.000000 tau_4_t))
(assert (<= tau_4_t 200.000000))
(assert (<= 0.000000 tau_5_0))
(assert (<= tau_5_0 200.000000))
(assert (<= 0.000000 tau_5_t))
(assert (<= tau_5_t 200.000000))
(assert (<= -4.000000 omega2_0_0))
(assert (<= omega2_0_0 4.000000))
(assert (<= -4.000000 omega2_0_t))
(assert (<= omega2_0_t 4.000000))
(assert (<= -4.000000 omega2_1_0))
(assert (<= omega2_1_0 4.000000))
(assert (<= -4.000000 omega2_1_t))
(assert (<= omega2_1_t 4.000000))
(assert (<= -4.000000 omega2_2_0))
(assert (<= omega2_2_0 4.000000))
(assert (<= -4.000000 omega2_2_t))
(assert (<= omega2_2_t 4.000000))
(assert (<= -4.000000 omega2_3_0))
(assert (<= omega2_3_0 4.000000))
(assert (<= -4.000000 omega2_3_t))
(assert (<= omega2_3_t 4.000000))
(assert (<= -4.000000 omega2_4_0))
(assert (<= omega2_4_0 4.000000))
(assert (<= -4.000000 omega2_4_t))
(assert (<= omega2_4_t 4.000000))
(assert (<= -4.000000 omega2_5_0))
(assert (<= omega2_5_0 4.000000))
(assert (<= -4.000000 omega2_5_t))
(assert (<= omega2_5_t 4.000000))
(assert (<= -4.000000 omega1_0_0))
(assert (<= omega1_0_0 4.000000))
(assert (<= -4.000000 omega1_0_t))
(assert (<= omega1_0_t 4.000000))
(assert (<= -4.000000 omega1_1_0))
(assert (<= omega1_1_0 4.000000))
(assert (<= -4.000000 omega1_1_t))
(assert (<= omega1_1_t 4.000000))
(assert (<= -4.000000 omega1_2_0))
(assert (<= omega1_2_0 4.000000))
(assert (<= -4.000000 omega1_2_t))
(assert (<= omega1_2_t 4.000000))
(assert (<= -4.000000 omega1_3_0))
(assert (<= omega1_3_0 4.000000))
(assert (<= -4.000000 omega1_3_t))
(assert (<= omega1_3_t 4.000000))
(assert (<= -4.000000 omega1_4_0))
(assert (<= omega1_4_0 4.000000))
(assert (<= -4.000000 omega1_4_t))
(assert (<= omega1_4_t 4.000000))
(assert (<= -4.000000 omega1_5_0))
(assert (<= omega1_5_0 4.000000))
(assert (<= -4.000000 omega1_5_t))
(assert (<= omega1_5_t 4.000000))
(assert (<= 0.000000 time_0))
(assert (<= time_0 200.000000))
(assert (<= 0.000000 time_1))
(assert (<= time_1 200.000000))
(assert (<= 0.000000 time_2))
(assert (<= time_2 200.000000))
(assert (<= 0.000000 time_3))
(assert (<= time_3 200.000000))
(assert (<= 0.000000 time_4))
(assert (<= time_4 200.000000))
(assert (<= 0.000000 time_5))
(assert (<= time_5 200.000000))
(assert (<= 1.000000 mode_0))
(assert (<= mode_0 3.000000))
(assert (<= 1.000000 mode_1))
(assert (<= mode_1 3.000000))
(assert (<= 1.000000 mode_2))
(assert (<= mode_2 3.000000))
(assert (<= 1.000000 mode_3))
(assert (<= mode_3 3.000000))
(assert (<= 1.000000 mode_4))
(assert (<= mode_4 3.000000))
(assert (<= 1.000000 mode_5))
(assert (<= mode_5 3.000000))
(assert (and (and (= omega2_0_0 2.500000) (= omega1_0_0 2.000000) (= tau_0_0 0.000000) (= z_0_0 0.000000) (= y_0_0 0.000000) (>= x_0_0 -0.200000) (<= x_0_0 0.100000)) (= mode_0 1.000000) (= [z_0_t y_0_t x_0_t tau_0_t omega2_0_t omega1_0_t] (integral 0. time_0 [z_0_0 y_0_0 x_0_0 tau_0_0 omega2_0_0 omega1_0_0] flow_1)) (= mode_0 1.000000) (forall_t 1.000000 [0.000000 time_0] (>= x_0_t -5.000000)) (>= x_0_t -5.000000) (>= x_0_0 -5.000000) (forall_t 1.000000 [0.000000 time_0] (>= y_0_t -5.000000)) (>= y_0_t -5.000000) (>= y_0_0 -5.000000) (forall_t 1.000000 [0.000000 time_0] (>= z_0_t -5.000000)) (>= z_0_t -5.000000) (>= z_0_0 -5.000000) (forall_t 1.000000 [0.000000 time_0] (>= omega1_0_t -3.140000)) (>= omega1_0_t -3.140000) (>= omega1_0_0 -3.140000) (forall_t 1.000000 [0.000000 time_0] (>= omega2_0_t -3.140000)) (>= omega2_0_t -3.140000) (>= omega2_0_0 -3.140000) (forall_t 1.000000 [0.000000 time_0] (<= tau_0_t 5.000000)) (<= tau_0_t 5.000000) (<= tau_0_0 5.000000) (= mode_1 2.000000) (>= tau_0_t 4.000000) (= omega2_1_0 1.000000) (= omega1_1_0 1.500000) (= z_1_0 z_0_t) (= y_1_0 (* y_0_t 0.200000)) (= x_1_0 x_0_t) (= tau_1_0 0.000000) (= [z_1_t y_1_t x_1_t tau_1_t omega2_1_t omega1_1_t] (integral 0. time_1 [z_1_0 y_1_0 x_1_0 tau_1_0 omega2_1_0 omega1_1_0] flow_2)) (= mode_1 2.000000) (forall_t 2.000000 [0.000000 time_1] (>= x_1_t -5.000000)) (>= x_1_t -5.000000) (>= x_1_0 -5.000000) (forall_t 2.000000 [0.000000 time_1] (>= y_1_t -5.000000)) (>= y_1_t -5.000000) (>= y_1_0 -5.000000) (forall_t 2.000000 [0.000000 time_1] (>= z_1_t -5.000000)) (>= z_1_t -5.000000) (>= z_1_0 -5.000000) (forall_t 2.000000 [0.000000 time_1] (>= omega1_1_t -3.140000)) (>= omega1_1_t -3.140000) (>= omega1_1_0 -3.140000) (forall_t 2.000000 [0.000000 time_1] (>= omega2_1_t -3.140000)) (>= omega2_1_t -3.140000) (>= omega2_1_0 -3.140000) (forall_t 2.000000 [0.000000 time_1] (<= tau_1_t 10.000000)) (<= tau_1_t 10.000000) (<= tau_1_0 10.000000) (= mode_2 3.000000) (>= tau_1_t 8.000000) (= omega2_2_0 (- 0.000000 omega2_1_t)) (= omega1_2_0 (sin omega1_1_t)) (= z_2_0 z_1_t) (= y_2_0 (* y_1_t 0.500000)) (= x_2_0 (* 0.200000 x_1_t)) (= tau_2_0 0.000000) (= [z_2_t y_2_t x_2_t tau_2_t omega2_2_t omega1_2_t] (integral 0. time_2 [z_2_0 y_2_0 x_2_0 tau_2_0 omega2_2_0 omega1_2_0] flow_3)) (= mode_2 3.000000) (forall_t 3.000000 [0.000000 time_2] (>= x_2_t -5.000000)) (>= x_2_t -5.000000) (>= x_2_0 -5.000000) (forall_t 3.000000 [0.000000 time_2] (>= y_2_t -5.000000)) (>= y_2_t -5.000000) (>= y_2_0 -5.000000) (forall_t 3.000000 [0.000000 time_2] (>= z_2_t -5.000000)) (>= z_2_t -5.000000) (>= z_2_0 -5.000000) (forall_t 3.000000 [0.000000 time_2] (>= omega1_2_t -3.140000)) (>= omega1_2_t -3.140000) (>= omega1_2_0 -3.140000) (forall_t 3.000000 [0.000000 time_2] (>= omega2_2_t -3.140000)) (>= omega2_2_t -3.140000) (>= omega2_2_0 -3.140000) (forall_t 3.000000 [0.000000 time_2] (<= tau_2_t 6.000000)) (<= tau_2_t 6.000000) (<= tau_2_0 6.000000) (= mode_3 1.000000) (>= tau_2_t 5.000000) (= omega2_3_0 1.000000) (= omega1_3_0 1.000000) (= z_3_0 z_2_t) (= y_3_0 y_2_t) (= x_3_0 x_2_t) (= tau_3_0 0.000000) (= [z_3_t y_3_t x_3_t tau_3_t omega2_3_t omega1_3_t] (integral 0. time_3 [z_3_0 y_3_0 x_3_0 tau_3_0 omega2_3_0 omega1_3_0] flow_1)) (= mode_3 1.000000) (forall_t 1.000000 [0.000000 time_3] (>= x_3_t -5.000000)) (>= x_3_t -5.000000) (>= x_3_0 -5.000000) (forall_t 1.000000 [0.000000 time_3] (>= y_3_t -5.000000)) (>= y_3_t -5.000000) (>= y_3_0 -5.000000) (forall_t 1.000000 [0.000000 time_3] (>= z_3_t -5.000000)) (>= z_3_t -5.000000) (>= z_3_0 -5.000000) (forall_t 1.000000 [0.000000 time_3] (>= omega1_3_t -3.140000)) (>= omega1_3_t -3.140000) (>= omega1_3_0 -3.140000) (forall_t 1.000000 [0.000000 time_3] (>= omega2_3_t -3.140000)) (>= omega2_3_t -3.140000) (>= omega2_3_0 -3.140000) (forall_t 1.000000 [0.000000 time_3] (<= tau_3_t 5.000000)) (<= tau_3_t 5.000000) (<= tau_3_0 5.000000) (= mode_4 2.000000) (>= tau_3_t 4.000000) (= omega2_4_0 1.000000) (= omega1_4_0 1.500000) (= z_4_0 z_3_t) (= y_4_0 (* y_3_t 0.200000)) (= x_4_0 x_3_t) (= tau_4_0 0.000000) (= [z_4_t y_4_t x_4_t tau_4_t omega2_4_t omega1_4_t] (integral 0. time_4 [z_4_0 y_4_0 x_4_0 tau_4_0 omega2_4_0 omega1_4_0] flow_2)) (= mode_4 2.000000) (forall_t 2.000000 [0.000000 time_4] (>= x_4_t -5.000000)) (>= x_4_t -5.000000) (>= x_4_0 -5.000000) (forall_t 2.000000 [0.000000 time_4] (>= y_4_t -5.000000)) (>= y_4_t -5.000000) (>= y_4_0 -5.000000) (forall_t 2.000000 [0.000000 time_4] (>= z_4_t -5.000000)) (>= z_4_t -5.000000) (>= z_4_0 -5.000000) (forall_t 2.000000 [0.000000 time_4] (>= omega1_4_t -3.140000)) (>= omega1_4_t -3.140000) (>= omega1_4_0 -3.140000) (forall_t 2.000000 [0.000000 time_4] (>= omega2_4_t -3.140000)) (>= omega2_4_t -3.140000) (>= omega2_4_0 -3.140000) (forall_t 2.000000 [0.000000 time_4] (<= tau_4_t 10.000000)) (<= tau_4_t 10.000000) (<= tau_4_0 10.000000) (= mode_5 3.000000) (>= tau_4_t 8.000000) (= omega2_5_0 (- 0.000000 omega2_4_t)) (= omega1_5_0 (sin omega1_4_t)) (= z_5_0 z_4_t) (= y_5_0 (* y_4_t 0.500000)) (= x_5_0 (* 0.200000 x_4_t)) (= tau_5_0 0.000000) (= [z_5_t y_5_t x_5_t tau_5_t omega2_5_t omega1_5_t] (integral 0. time_5 [z_5_0 y_5_0 x_5_0 tau_5_0 omega2_5_0 omega1_5_0] flow_3)) (= mode_5 3.000000) (forall_t 3.000000 [0.000000 time_5] (>= x_5_t -5.000000)) (>= x_5_t -5.000000) (>= x_5_0 -5.000000) (forall_t 3.000000 [0.000000 time_5] (>= y_5_t -5.000000)) (>= y_5_t -5.000000) (>= y_5_0 -5.000000) (forall_t 3.000000 [0.000000 time_5] (>= z_5_t -5.000000)) (>= z_5_t -5.000000) (>= z_5_0 -5.000000) (forall_t 3.000000 [0.000000 time_5] (>= omega1_5_t -3.140000)) (>= omega1_5_t -3.140000) (>= omega1_5_0 -3.140000) (forall_t 3.000000 [0.000000 time_5] (>= omega2_5_t -3.140000)) (>= omega2_5_t -3.140000) (>= omega2_5_0 -3.140000) (forall_t 3.000000 [0.000000 time_5] (<= tau_5_t 6.000000)) (<= tau_5_t 6.000000) (<= tau_5_0 6.000000) (= mode_5 3.000000) (= tau_5_t 4.000000)))
(check-sat)
(exit)
```

## Result

<script src="/js/d3.v3.js"></script>
<script src="/js/underscore-min.js"></script>
<div id="chart-container" style="text-align:center">
<script type="text/javascript" src="/benchmarks/electronic_oscillator/data.js"></script>
<script type="text/javascript" src="/js/vis.js"></script>
</div>
