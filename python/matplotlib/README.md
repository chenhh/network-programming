# matplotlib

## 簡介

matplotlib是一個強大的繪圖函式庫，但我在使用時，經常會忘記個別組件在圖表上的名稱與使用的方法，因此本文的重點在於以重點筆記的方式說明各組件的名稱與互動的方法。

matplotlib 的 API （Application Programming Interface）共分成兩種型態，一種是我們常見到的 plt.plot 或是 df.plot 的格式，另一種則是 ax.plot 的格式。

* `plt.plot`：繪圖的懶人包（包括 `df.plot` ），會幫你直接在最近使用的圖表上繪圖，沒有的話就會自動新建一個。 `plt.plot` 其實是一個黑盒子，他幫你把基礎的參數設定好，他就會在最近一張子圖生成圖表（沒有則會創建一張）；但這不代表背後就沒有 `figure` 和 `axes` 的運作。
* `ax.plot`：手動建立的 API，提供多項客製化的參數與圖表控制。

```python
# 直接將繪圖的所有組件全部用plt處理，不必管figure與axes的細節
import matplotlib.pyplot as plt
import numpy as np

x = np.linspace(0, 2, 100)

plt.plot(x, x, label='linear')
plt.plot(x, x**2, label='quadratic')
plt.plot(x, x**3, label='cubic')

plt.xlabel('x label')
plt.ylabel('y label')
plt.title("Simple Plot")
plt.legend()
plt.show()
```

![plt直接繪圖](../../.gitbook/assets/plt\_plot-min.png)

```python
import matplotlib.pyplot as plt
import numpy as np
# 將 figure 例項化到 fig 的變數上，並設定寬與高（此處為預設值）
fig = plt.figure(figsize=(6, 4))

# 將 axe 新增到例項化後 2×2 的 figure 上，並指定第 1,2,3 個
ax_1 = fig.add_subplot(2, 2, 1)
ax_2 = fig.add_subplot(2, 2, 2)
ax_3 = fig.add_subplot(2, 2, 3)
plt.show()

# 以下程式碼有相同的結果
fig = plt.figure(num=4, figsize=(6, 4))
plt.subplot(221)
plt.subplot(222)
plt.subplot(223)
plt.show()
```

![以axes繪圖，較為複雜](../../.gitbook/assets/plt\_ax-min.png)

* 第一種方式plt，是先生成了一個畫布，然後在這個畫布上隱式的生成一個畫圖區域來進行畫圖。
* 第二種方式axes，先生成一個畫布，然後，我們在此畫布上，選定一個子區域畫了一個子圖。



## 組件

* Figure：可以把他當作畫布，一張畫布上可以有很多(至少一個)的 Axes。 也會包含了客制化的legend, titles等組件。
* Axes：就是我們俗稱的「子圖」，每個 Axes 一次只能在一張畫布上。這是實際繪圖的部份，Axes包含至少兩個Axis物件，其負責資料限制(`set_xlim()`, `set_ylim()等`)，每個Axes都有一個標題物件(title)，可透過`set_title()`設定。一個x軸標籤(透過`set_xlabel()`設定)，一個y軸標籤(透過`set_ylabel()`設定)。
* Axis：類似數字線的物件，負責圖形限制與生成軸的刻度(tick)的刻度線標記(tick labels) 。刻度的位置由Locator物件所決定，而刻度線標記由Formatter物件標記。

![各組件名稱](<../../.gitbook/assets/matplotlib\_widget-min (1).png>)

![matplotlib組件](../../.gitbook/assets/matplotlib\_widget.jpg)

## 參考資料

* [official site](https://matplotlib.org/)
* [online matplotlib compiler](https://www.tutorialspoint.com/execute\_matplotlib\_online.php)
