import os
from building import *

# enable all module by default
ACTIVATION = True
BASICMATHSNN = True
CONCATENATION = True
CONVOLUTION = True
FULLYCONNECTED = True
LSTM = True
POOLING = True
RESHAPE = True
SOFTMAX = True
SVDF = True

# CMSIS-NN papckage Kconfig option value
USE_CMSIS_NN_CONFIG = GetDepend(['PKG_USING_CMSIS_NN'])

# Kconfig sourced, and CMSIS-NN package enabled
if USE_CMSIS_NN_CONFIG:
    ACTIVATION = GetDepend(['CMSIS_NN_ACTIVATION'])
    BASICMATHSNN = GetDepend(['CMSIS_NN_BASICMATHSNN'])
    CONCATENATION = GetDepend(['CMSIS_NN_CONCATENATION'])
    CONVOLUTION = GetDepend(['CMSIS_NN_CONVOLUTION'])
    FULLYCONNECTED = GetDepend(['CMSIS_NN_FULLYCONNECTED'])
    LSTM = GetDepend(['CMSIS_NN_LSTM'])
    POOLING = GetDepend(['CMSIS_NN_POOLING'])
    RESHAPE = GetDepend(['CMSIS_NN_RESHAPE'])
    SOFTMAX = GetDepend(['CMSIS_NN_SOFTMAX'])
    SVDF = GetDepend(['CMSIS_NN_SVDF'])

# Always needed if any other module above is on.
NNSUPPORT = ACTIVATION or BASICMATHSNN or CONCATENATION or CONVOLUTION or \
    FULLYCONNECTED or LSTM or POOLING or RESHAPE or SOFTMAX or SVDF

submodules = (
    (ACTIVATION, 'ActivationFunctions'),
    (BASICMATHSNN, 'BasicMathFunctions'),
    (CONCATENATION, 'ConcatenationFunctions'),
    (CONVOLUTION, 'ConvolutionFunctions'),
    (FULLYCONNECTED, 'FullyConnectedFunctions'),
    (LSTM, 'LSTMFunctions'),
    (NNSUPPORT, 'NNSupportFunctions'),
    (POOLING, 'PoolingFunctions'),
    (RESHAPE, 'ReshapeFunctions'),
    (SOFTMAX, 'SoftmaxFunctions'),
    (SVDF, 'SVDFunctions')
)

# print('USE_CMSIS_NN_CONFIG=', USE_CMSIS_NN_CONFIG)
# print('submodules=', submodules)
cwd = GetCurrentDir()

CPPPATH = [cwd + '/Include']
SOURCES = []

for m in submodules:
    if m[0]:
        SOURCES += Glob('Source/' + m[1] + '/*.c')

LOCAL_CCFLAGS = ["-Ofast"]

objs = DefineGroup(name='CMSIS-NN', src=SOURCES, depend=[''],
                   CPPPATH=CPPPATH,
                   LOCAL_CCFLAGS=LOCAL_CCFLAGS)


# CMSIS-NN papckage Kconfig PKG_USING_CMSIS_NN_TESTS option value
USE_CMSIS_NN_TESTS = GetDepend(['PKG_USING_CMSIS_NN_TESTS'])
# print('USE_CMSIS_NN_TESTS = ', USE_CMSIS_NN_TESTS)

if USE_CMSIS_NN_TESTS:
    tests = cwd + '/Tests'
    ents = os.listdir(tests)
    for item in ents:
        sconsfile = os.path.join(tests, item, 'SConscript')
        if os.path.isfile(sconsfile):
            objs += SConscript(sconsfile)

Return('objs')
