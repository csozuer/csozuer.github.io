```python
import matplotlib.pyplot as plt 
from scipy.fft import fft, fftfreq
import pydub
import numpy as np
```


```python
#https://stackoverflow.com/questions/53633177/how-to-read-a-mp3-audio-file-into-a-numpy-array-save-a-numpy-array-to-mp3
def read(f, normalized=False):
    """MP3 to numpy array"""
    a = pydub.AudioSegment.from_mp3(f)
    y = np.array(a.get_array_of_samples())
    if a.channels == 2:
        y = y.reshape((-1, 2))
    if normalized:
        return a.frame_rate, np.float32(y) / 2**15
    else:
        return a.frame_rate, y
```


```python
audio = read('furelise.mp3')
```


```python
audio[1][:,0]
```




    array([ 0,  0,  0, ...,  1, -4, -2], dtype=int16)




```python
len(audio[1][:,0])
```




    9353216




```python
audio
```




    (44100,
     array([[ 0,  0],
            [ 0,  0],
            [ 0,  0],
            ...,
            [ 1,  1],
            [-4,  2],
            [-2, -1]], dtype=int16))




```python
audio_l = audio[1][:,0]
```


```python
plt.plot(audio[1][:,0])
```




    [<matplotlib.lines.Line2D at 0x7fd6174e9670>]






    
![png](fft%20_files/fft%20_7_1.png)
    




```python
fft_plot = fft(audio_l[0:128000])
```


```python
fft_plot
```




    array([-1133545.            -0.j        ,
             -20011.90780619-58321.61632916j,
            -682817.19484499-82391.24766122j, ...,
              63269.08681399-22631.50656288j,
            -682817.19484499+82391.24766122j,
             -20011.90780619+58321.61632916j])




```python
plt.plot(np.abs(fft_plot))
```




    [<matplotlib.lines.Line2D at 0x7fd63636df40>]






    
![png](fft%20_files/fft%20_10_1.png)
    




```python

```
