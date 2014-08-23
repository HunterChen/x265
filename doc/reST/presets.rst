Preset Options
--------------

Presets
=======

.. _preset-tune-ref:

x265 has a number of predefined :option:`--preset` options that make
trade-offs between encode speed (encoded frames per second) and
compression efficiency (quality per bit in the bitstream).  The default
preset is medium, it does a reasonably good job of finding the best
possible quality without spending enormous CPU cycles looking for the
absolute most efficient way to achieve that quality.  As you go higher
than medium, the encoder takes shortcuts to improve performance at the
expense of quality and compression efficiency.  As you go lower than
medium, the encoder tries harder and harder to achieve the best quailty
per bit compression ratio.

The presets adjust encoder parameters to affect these trade-offs.

+--------------+-----------+-----------+----------+--------+------+--------+------+--------+----------+---------+
|              | ultrafast | superfast | veryfast | faster | fast | medium | slow | slower | veryslow | placebo |
+==============+===========+===========+==========+========+======+========+======+========+==========+=========+
| ctu          |   32      |    32     |   32     |  64    |  64  |   64   |  64  |  64    |   64     |   64    |
+--------------+-----------+-----------+----------+--------+------+--------+------+--------+----------+---------+
| bframes      |    4      |     4     |    4     |   4    |  4   |    4   |  4   |   8    |    8     |    8    |
+--------------+-----------+-----------+----------+--------+------+--------+------+--------+----------+---------+
| b-adapt      |    0      |     0     |    0     |   0    |  2   |    2   |  2   |   2    |    2     |    2    |
+--------------+-----------+-----------+----------+--------+------+--------+------+--------+----------+---------+
| rc-lookahead |   10      |    10     |   15     |  15    |  15  |   20   |  25  |   30   |   40     |   60    |
+--------------+-----------+-----------+----------+--------+------+--------+------+--------+----------+---------+
| scenecut     |    0      |    40     |   40     |  40    |  40  |   40   |  40  |   40   |   40     |   40    |
+--------------+-----------+-----------+----------+--------+------+--------+------+--------+----------+---------+
| refs         |    1      |     1     |    1     |   1    |  3   |    3   |  3   |   3    |    5     |    5    |
+--------------+-----------+-----------+----------+--------+------+--------+------+--------+----------+---------+
| me           |   dia     |   hex     |   hex    |  hex   | hex  |   hex  | star |  star  |   star   |   star  |
+--------------+-----------+-----------+----------+--------+------+--------+------+--------+----------+---------+
| merange      |   25      |    44     |   57     |  57    |  57  |   57   | 57   |  57    |   57     |   92    |
+--------------+-----------+-----------+----------+--------+------+--------+------+--------+----------+---------+
| subme        |    0      |     1     |    1     |   2    |  2   |    2   |  3   |   3    |    4     |    5    |
+--------------+-----------+-----------+----------+--------+------+--------+------+--------+----------+---------+
| rect         |    0      |     0     |    0     |   0    |  0   |    0   |  1   |   1    |    1     |    1    |
+--------------+-----------+-----------+----------+--------+------+--------+------+--------+----------+---------+
| amp          |    0      |     0     |    0     |   0    |  0   |    0   |  0   |   1    |    1     |    1    |
+--------------+-----------+-----------+----------+--------+------+--------+------+--------+----------+---------+
| max-merge    |    2      |     2     |    2     |   2    |  2   |    2   |  3   |   3    |    4     |    5    |
+--------------+-----------+-----------+----------+--------+------+--------+------+--------+----------+---------+
| early-skip   |    1      |     1     |    1     |   1    |  0   |    0   |  0   |   0    |    0     |    0    |
+--------------+-----------+-----------+----------+--------+------+--------+------+--------+----------+---------+
| fast-intra   |    1      |     1     |    1     |   1    |  1   |    0   |  0   |   0    |    0     |    0    |
+--------------+-----------+-----------+----------+--------+------+--------+------+--------+----------+---------+
| fast-cbf     |    1      |     1     |    1     |   1    |  0   |    0   |  0   |   0    |    0     |    0    |
+--------------+-----------+-----------+----------+--------+------+--------+------+--------+----------+---------+
| sao          |    0      |     1     |    1     |   1    |  1   |    1   |  1   |   1    |    1     |    1    |
+--------------+-----------+-----------+----------+--------+------+--------+------+--------+----------+---------+
| signhide     |    0      |     1     |    1     |   1    |  1   |    1   |  1   |   1    |    1     |    1    |
+--------------+-----------+-----------+----------+--------+------+--------+------+--------+----------+---------+
| weightp      |    0      |     0     |    1     |   1    |  1   |    1   |  1   |   1    |    1     |    1    |
+--------------+-----------+-----------+----------+--------+------+--------+------+--------+----------+---------+
| aq-mode      |    0      |     0     |    2     |   2    |  2   |    2   |  2   |   2    |    2     |    2    |
+--------------+-----------+-----------+----------+--------+------+--------+------+--------+----------+---------+
| cuTree       |    0      |     0     |    0     |   0    |  1   |    1   |  1   |   1    |    1     |    1    |
+--------------+-----------+-----------+----------+--------+------+--------+------+--------+----------+---------+
| rdLevel      |    2      |     2     |    2     |   2    |  2   |    3   |  4   |   6    |    6     |    6    |
+--------------+-----------+-----------+----------+--------+------+--------+------+--------+----------+---------+
| lft          |    0      |     1     |    1     |   1    |  1   |    1   |  1   |   1    |    1     |    1    |
+--------------+-----------+-----------+----------+--------+------+--------+------+--------+----------+---------+
| tu-intra     |    1      |     1     |    1     |   1    |  1   |    1   |  1   |   2    |    3     |    4    |
+--------------+-----------+-----------+----------+--------+------+--------+------+--------+----------+---------+
| tu-inter     |    1      |     1     |    1     |   1    |  1   |    1   |  1   |   2    |    3     |    4    |
+--------------+-----------+-----------+----------+--------+------+--------+------+--------+----------+---------+

Placebo mode further enables transform-skip prediction analysis
(lossless).

Tuning
======

There are a few :option:`--tune` options available, which are applied
after the preset.

.. Note::

	The *psnr* and *ssim* tune options disable all optimizations that
	sacrafice metric scores for perceived visual quality (also known as
	psycho-visual optimizations). By default x265 always tunes for
	highest perceived visual quality but if one intends to measure an
	encode using PSNR or SSIM for the purpose of benchmarking, we highly
	recommend you configure x265 to tune for that particular metric.

+--------------+-----------------------------------------------------+
| --tune       | effect                                              |
+==============+=====================================================+
| psnr         | disables adaptive quant, psy-rd, and cutree         |
+--------------+-----------------------------------------------------+
| ssim         | enables adaptive quant auto-mode, disables psy-rd   |
+--------------+-----------------------------------------------------+
| fastdecode   | no loop filters, no weighted pred, no intra in B    |
+--------------+-----------------------------------------------------+
| zerolatency  | no lookahead, no B frames, no cutree                |
+--------------+-----------------------------------------------------+