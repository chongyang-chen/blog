---
title: 计算三角形的面积
date: 2020-11-24 19:52:04
categories:
- 数学
tags:
- 面积
---

平面内随机取三个点，计算三个点组成的三角形的面积。

使用到C语言随机函数，数学上的距离公式，面积公式等。

<!-- more -->

核心代码：

```c
double trangleArea(const double a, const double b, const double c){
    double p = (a + b + c) / 2;
    double q = p*(p - a)*(p - b)*(p - c);
    if (q < 0) {
        return 0.0;
    }
    return sqrt(q);
}
```



展示了点的坐标，三条边的长度以及三角形的面积。

```shell
( 32.19, 77.17),( 43.58, 65.93),( 72.80, 29.07),
( 47.0369, 62.9506, 16.0022),area = 45.7013

( 99.02, 45.69),( 93.88,  8.13),( 96.83, 54.78),
( 46.7432,  9.3501, 37.9101),area = 64.4895

( 17.22, 97.74),( 12.47, 46.54),( 52.31, 80.73),
( 52.4993, 38.9955, 51.4199),area = 938.7028

( 79.83, 42.43),( 80.30, 70.47),( 23.33, 94.69),
( 61.9047, 76.9634, 28.0439),area = 804.4111

( 70.44, 14.87),( 74.20, 31.71),( 65.63, 29.99),
(  8.7409, 15.8666, 17.2547),area = 68.9258

( 55.85, 90.95),( 27.81, 54.63),(  7.88, 45.26),
( 22.0228, 66.2472, 45.8845),area = 230.5614

( 31.96, 10.11),( 95.94, 47.12),( 92.88, 52.96),
(  6.5931, 74.4807, 73.9133),area = 243.4469

( 95.45, 46.66),(  8.15, 99.22),(  9.58, 14.64),
( 84.5921, 91.6457,101.9011),area = 3654.3366

( 99.58, 15.21),(  8.75, 96.59),( 30.41, 94.92),
( 21.7243,105.5375,121.9541),area = 805.5023

( 31.68, 11.33),( 22.91, 24.70),(  9.04, 73.84),
( 51.0599, 66.4836, 15.9897),area = 122.7579

( 36.02, 21.55),( 38.33, 91.13),( 99.12, 44.97),
( 76.3294, 67.3061, 69.6183),area = 2168.1989

( 74.46, 70.18),( 50.65, 74.04),( 94.28, 11.96),
( 75.8782, 61.5012, 24.1209),area = 654.8565

( 49.26, 56.29),( 56.04, 33.52),( 74.73, 32.50),
( 18.7178, 34.8523, 23.7580),area = 209.3278

( 89.73, 83.56),( 73.97, 21.76),( 71.31, 69.68),
( 47.9938, 23.0641, 63.7779),area = 459.8036

( 18.57, 25.17),( 39.27, 72.24),( 38.03,  9.50),
( 62.7523, 24.9848, 51.4206),area = 620.1756

( 45.20,  0.16),( 73.93, 44.60),( 50.29,  9.10),
( 42.6509, 10.2875, 52.9181),area = 15.3233

( 33.74, 20.03),( 70.66, 28.55),( 62.48, 90.41),
( 62.3985, 76.0219, 37.8903),area = 1176.7824

( 62.62, 17.34),( 24.44, 76.76),( 22.28, 93.04),
( 16.4227, 85.7777, 70.6290),area = 246.6116

( 36.51, 56.66),( 39.08, 27.73),( 19.96,  9.32),
( 26.5425, 50.1496, 29.0439),area = 300.2277

( 55.95, 78.27),( 78.92, 81.66),( 63.84,  7.65),
( 75.5307, 71.0594, 23.2188),area = 824.4443

( 72.74,  0.76),( 84.34, 44.92),(  3.84, 91.54),
( 93.0251,113.9659, 45.6581),area = 2047.8360

(  0.90, 72.73),( 16.41, 64.40),( 31.89, 19.10),
( 47.8719, 61.9399, 17.6054),area = 286.8273

( 23.99, 83.56),( 54.43, 45.00),( 78.92, 78.96),
( 41.8693, 55.1223, 49.1271),area = 989.0384

( 42.19, 73.80),( 16.99, 27.95),(  8.62, 88.56),
( 61.1852, 36.6715, 52.3189),area = 955.5682

( 78.00, 20.04),( 94.24, 34.72),( 36.40, 52.57),
( 60.5317, 52.8087, 21.8916),area = 569.4876

( 36.94, 86.51),( 52.70, 66.32),( 93.68, 38.35),
( 49.6153, 74.4232, 25.6128),area = 193.2895

( 95.10, 72.86),( 38.32, 12.45),( 85.78, 39.39),
( 54.5730, 34.7434, 82.9056),area = 668.7027

(  7.59, 73.75),( 74.61, 97.85),( 43.02, 44.62),
( 61.8980, 45.8677, 71.2214),area = 1403.0778

( 25.74, 20.16),( 62.73, 55.86),( 78.44, 91.07),
( 38.5558, 88.3488, 51.4077),area = 370.7855

( 18.68, 68.95),( 14.99, 22.00),( 88.43,  2.32),
( 76.0312, 96.4605, 47.0948),area = 1760.3136

( 75.13, 23.44),( 92.16, 29.61),( 79.31, 41.17),
( 17.2846, 18.2161, 18.1132),area = 138.0757

( 97.64, 26.25),(  7.96,  6.33),( 75.20, 58.90),
( 85.3512, 39.6179, 91.8657),area = 1687.5284

( 94.61, 87.92),( 90.86,  1.68),( 70.97,  3.16),
( 19.9450, 87.9949, 86.3215),area = 860.4318

( 87.57,  5.26),( 14.46,  3.77),( 25.03, 49.55),
( 46.9844, 76.6346, 73.1252),area = 1665.6132

( 71.51, 94.44),( 16.49,  0.02),( 90.77, 76.07),
(106.3067, 26.6159,109.2810),area = 1414.6233

( 81.34, 20.05),( 60.82, 78.12),( 41.93, 93.79),
( 24.5435, 83.6106, 61.5889),area = 387.6969

( 77.84, 91.43),( 13.29, 87.14),( 13.90, 77.24),
(  9.9188, 65.4956, 64.6924),area = 320.8310

( 31.01, 46.91),(  5.80,  0.59),( 81.17, 68.42),
(101.3980, 54.5775, 52.7360),area = 890.5720

( 15.78, 81.87),( 36.28, 74.63),( 68.46, 78.18),
( 32.3752, 52.8091, 21.7409),area = 152.8791

( 67.02, 98.02),( 26.59, 48.48),( 19.80, 59.79),
( 13.1917, 60.7558, 63.9437),area = 396.8199

( 33.50, 63.12),( 68.92, 92.76),( 65.51, 69.11),
( 23.8946, 32.5656, 46.1856),area = 368.3053

( 13.04,  7.70),( 60.05, 64.25),( 69.39, 62.66),
(  9.4744, 78.7142, 73.5380),area = 301.4614

( 53.78, 69.46),( 44.99, 57.99),( 42.06, 74.31),
( 16.5809, 12.6839, 14.4508),area = 88.5299

( 73.66, 14.07),( 64.47, 47.77),( 85.45, 47.12),
( 20.9901, 35.0900, 34.9306),area = 350.5262

( 63.81, 64.94),( 94.06, 42.03),( 25.86, 37.48),
( 68.3516, 46.8429, 37.9464),area = 850.0497

( 56.04, 80.39),( 35.62, 13.05),( 77.18, 96.16),
( 92.9220, 26.3741, 70.3680),area = 550.7721

(  0.03, 90.44),( 71.49, 74.87),( 26.40, 69.43),
( 45.4170, 33.7164, 73.1366),area = 545.3968

( 34.17, 61.89),( 32.60, 95.96),( 32.97, 13.65),
( 82.3108, 48.2549, 34.1062),area = 58.3104

( 10.05, 37.86),(  0.60, 62.42),( 75.77, 96.57),
( 82.5636, 88.1248, 26.3153),area = 1084.4464

( 16.35, 29.11),( 92.84, 23.67),( 48.38, 42.99),
( 48.4763, 34.9081, 76.6832),area = 617.9622

( 38.41, 42.48),( 13.35, 54.52),( 16.45, 90.07),
( 35.6849, 52.4123, 27.8023),area = 464.1035

( 10.80, 55.36),( 97.25, 74.68),( 83.36, 87.25),
( 18.7333, 79.2586, 88.5825),area = 677.5156

( 91.64, 65.83),( 42.53, 54.10),( 55.18, 37.93),
( 20.5303, 45.9101, 50.4914),area = 471.2466

( 19.46, 87.50),( 24.30, 33.26),(  3.33, 74.52),
( 46.2831, 20.7040, 54.4555),area = 468.8572

( 95.79, 21.24),( 57.96, 86.77),( 98.58, 79.28),
( 41.3048, 58.1070, 75.6656),area = 1189.2409

( 30.68, 21.91),(  0.19, 38.04),(  2.90, 78.70),
( 40.7502, 63.2205, 34.4937),area = 641.7178

( 93.85, 80.93),( 22.16,  6.78),( 33.92, 46.36),
( 41.2901, 69.1859,103.1391),area = 982.7431

( 30.84, 73.19),( 47.81, 23.73),( 93.31, 97.56),
( 86.7244, 67.0552, 52.2903),area = 1751.6625

( 80.94, 16.13),( 30.77, 58.26),( 98.28, 72.87),
( 69.0728, 59.3305, 65.5131),area = 1788.5900

( 31.10, 87.09),( 54.56, 45.82),( 71.61, 29.11),
( 23.8731, 70.7301, 47.4719),area = 155.8184

( 63.81, 52.15),( 91.73, 70.12),( 65.90, 42.38),
( 37.9038,  9.9910, 33.2031),area = 155.1678

( 36.99, 73.24),( 82.56, 38.60),(  0.36, 36.86),
( 82.2184, 51.6262, 57.2412),area = 1463.3499

(  7.93, 21.54),( 47.19, 72.71),( 49.22, 62.13),
( 10.7730, 57.9000, 64.4959),area = 259.6229

( 35.24, 63.38),( 24.76,  3.13),( 86.53,  9.54),
( 62.1017, 74.3600, 61.1547),area = 1827.2329

( 30.25, 77.39),( 39.49, 89.05),( 20.63,  6.38),
( 84.7940, 71.6587, 14.8773),area = 271.9816

(  7.16, 29.89),(  8.27, 65.88),( 27.04, 17.66),
( 51.7444, 23.3407, 36.0071),area = 364.5283

(  1.48, 39.90),( 70.04, 57.86),( 61.75, 95.15),
( 38.2004, 81.7621, 70.8734),area = 1352.7454

( 94.72, 43.39),( 11.26, 34.34),( 61.95,  2.32),
( 59.9563, 52.5416, 83.9492),area = 1565.5668

( 62.66, 69.95),( 91.69,  1.81),( 85.11, 96.10),
( 94.5193, 34.4648, 74.0662),area = 1144.4388

( 14.51, 49.39),( 99.99, 14.28),( 35.19,  2.19),
( 65.9182, 51.5316, 92.4096),area = 1654.2906

( 50.49, 44.29),( 13.79, 75.70),( 40.25, 35.62),
( 48.0264, 13.4174, 48.3061),area = 319.9137

( 40.10, 55.16),( 46.53, 59.96),( 26.52, 23.43),
( 41.6514, 34.5139,  8.0240),area = 69.4200

( 77.55, 78.40),( 15.08, 19.59),( 70.23, 22.21),
( 55.2122, 56.6648, 85.7970),area = 1539.8501

( 25.82, 35.77),( 19.79, 77.49),( 20.51, 80.21),
(  2.8137, 44.7561, 42.1535),area = 23.2200

( 13.62, 11.72),( 37.89, 56.19),( 63.89, 73.57),
( 31.2740, 79.7025, 50.6618),area = 367.2037

( 74.58,  6.91),( 70.33, 28.22),(  6.36, 60.63),
( 71.7117, 86.8321, 21.7297),area = 612.7291

( 26.31, 66.65),( 61.53, 32.77),(  3.13, 64.69),
( 66.5541, 23.2627, 48.8703),area = 427.1848

( 33.49, 44.01),( 18.43, 17.21),( 82.73, 32.75),
( 66.1512, 50.5110, 30.7416),area = 744.6038

( 98.37, 37.97),(  2.18, 91.54),( 96.55,  1.17),
(130.6615, 36.8450,110.1011),area = 1818.6447

( 92.10, 76.74),( 65.08, 50.33),( 74.98, 36.31),
( 17.1631, 43.9053, 37.7832),area = 320.1397

( 71.75, 58.33),( 16.63, 78.92),( 14.09, 16.29),
( 62.6815, 71.3585, 58.8401),area = 1752.2321

(  5.28, 68.03),( 52.64,  9.32),( 59.03, 42.36),
( 33.6522, 59.5652, 75.4310),area = 969.9657

( 37.46, 13.07),( 21.41, 73.36),( 30.36, 11.60),
( 62.4051,  7.2506, 62.3898),area = 225.8262

( 54.51, 96.95),( 30.08, 49.46),( 16.50, 49.23),
( 13.5819, 61.0079, 53.4053),area = 319.6476

( 86.42, 70.63),( 70.72,  9.76),( 13.20, 64.44),
( 79.3628, 73.4812, 62.8621),area = 2179.8592

( 22.63, 49.28),( 48.20, 91.15),(  3.79, 93.71),
( 44.4837, 48.2594, 49.0604),area = 962.4530

( 84.94, 87.55),( 79.91, 10.62),(  1.23, 82.40),
(106.5031, 83.8683, 77.0943),area = 3206.9529

( 99.29, 66.73),( 81.14, 28.68),( 49.19, 84.77),
( 64.5515, 53.2490, 42.1571),area = 1116.8655

( 90.06, 33.02),( 20.44, 85.89),(  4.30, 93.12),
( 17.6854,104.7224, 87.4196),area = 174.9846

( 98.47, 38.03),( 55.78,  5.62),( 71.84, 71.59),
( 67.8967, 42.8419, 53.5989),area = 1147.8774

( 79.78,  3.73),( 77.27, 15.07),(  9.37,  4.71),
( 68.6858, 70.4168, 11.6145),area = 397.9948

( 88.78, 56.51),( 24.98, 46.58),(  7.17, 56.37),
( 20.3234, 81.6101, 64.5681),area = 400.7277

( 35.48, 81.49),( 95.42, 81.74),( 10.52, 61.01),
( 87.3942, 32.2867, 59.9405),area = 610.6656

( 15.94, 59.67),( 89.45, 50.64),( 22.95, 51.02),
( 66.5011, 11.1338, 74.0625),area = 286.2806

( 72.35, 27.30),( 30.69, 45.07),( 58.48, 18.09),
( 38.7325, 16.6494, 45.2916),area = 315.0792

( 43.19,  0.60),( 51.94, 17.34),( 68.98, 65.95),
( 51.5101, 70.2549, 18.8889),area = 70.0439

( 56.28,  0.74),( 56.94, 74.42),( 86.70, 15.12),
( 66.3487, 33.6476, 73.6830),area = 1115.9274

( 59.24, 90.40),( 56.02, 56.39),( 29.10, 32.89),
( 35.7342, 64.9293, 34.1621),area = 419.9396

( 42.25, 37.88),( 79.32, 57.58),( 92.66, 77.51),
( 23.9825, 64.1226, 41.9795),area = 238.0036

( 58.56, 65.26),( 85.14, 34.68),( 92.87, 26.10),
( 11.5486, 52.0642, 40.5171),area = 4.1635
Program ended with exit code: 0
```
