# Oracle-50K
Oracle Character Recognition Dataset - Oracle-50K

|            | Num. of Instances | Num.of Classes
| ---------- | ----------------- | ---------- 
| Xiaoxuetang| 13255 | 1096
| Koukotsu   | 18671 | 1850
| Chinese Etymology | 27155 | 1120
| **Oracle-50K** | **59081** | **2668**

  Google Drive: https://drive.google.com/file/d/1PyXHz84viKr6N7GsWzrbPJubCkBBeLXv/view?usp=sharing

# Unlabeled Source Data
  The unlabeld source data for Unsupervised Few-Shot Oracle Character Recognition, including oracle and other ancient Chinese characters.\
  We use the online approximation algorithm from [[1]](https://arxiv.org/abs/2003.10593) to convert pixel images to sequence data. \
  Due to 3 failure cases during online approximation, the number of samples in pixel format and sequence format are 276,031 and 276,028, respectively.\
  \
  Google Drive: https://drive.google.com/file/d/1cn-LCIs61P5I26yMHboPdSTj0MOkgcUM/view?usp=sharing

# Oracle-FS
  The Few-Shot Oracle dataset for Unsupervised Few-Shot Oracle Character Recognition.\
  Oracle-FS is constructed from Oracle-50K by randomly choose 200 categories.\
  k-shot: k training examples and 20 test examples per class.\
  \
  Google Drive: https://drive.google.com/file/d/1EbK0zuNpUFYmfZVAq4nDmVWsy7REO4hx/view?usp=sharing\
 
 
 ```
  # A simple case for .npz file loading and sample visualization

  import numpy as np
  import random
  import matplotlib.pyplot as plt
 
  npz_path = 'xxx.npz'
  data = np.load(npz_path, encoding='latin1', allow_pickle=True)
  train_data = data['train']
  test_data = data['test']

  sample = np.random.choice(test_data, 1)[0]

  def strokes_to_lines(strokes):
    """Convert stroke-3 format to polyline format."""
    x = 0
    y = 0
    lines = []
    line = []

    for i in range(len(strokes)):
        if strokes[i, 2] == 1:
            x += float(strokes[i, 0])
            y += float(strokes[i, 1])
            line.append([x, y])
            lines.append(line)
            line = []
        else:
            x += float(strokes[i, 0])
            y += float(strokes[i, 1])
            line.append([x, y])
    return lines

  def show_one_sample(strokes, linewidth=100):
    lines = strokes_to_lines(strokes)
    for idx in range(0, len(lines)):
        x = [x[0] for x in lines[idx]]
        y = [y[1] for y in lines[idx]]
        plt.plot(x, y, 'k-', linewidth=linewidth)

    ax = plt.gca()
    plt.xticks([])
    plt.yticks([])
    ax.xaxis.set_ticks_position('top')
    ax.invert_yaxis()
   
   # show
   plot(sample)
  
 ```
