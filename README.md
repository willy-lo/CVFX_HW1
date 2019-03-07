# CVFX_HW1
1.Training progress:  
 
  Monet2photo	
  
  剛開始train的進度條 :

![image](https://github.com/willy-lo/CVFX_HW1/blob/master/cv_hw1/monet2photo.png)

 Summer2winter	
 
 剛開始train的進度條:
 
![image](https://github.com/willy-lo/CVFX_HW1/blob/master/cv_hw1/summer2winter1.png)

 train到99%時的進度條:
 
 ![image](https://github.com/willy-lo/CVFX_HW1/blob/master/cv_hw1/summer2winter99.png)
 
2.test our pictures

 選取test的圖片

 ![image](https://github.com/willy-lo/CVFX_HW1/blob/master/cv_hw1/test_summer.jpg)
 
 Test完的結果
 
 夏天變冬天:
 
 ![image](https://github.com/willy-lo/CVFX_HW1/blob/master/cv_hw1/test_before_after.png)
 
                     After                         Before
                          
 選取test的圖片      
 
 ![image](https://github.com/willy-lo/CVFX_HW1/blob/master/cv_hw1/test_winter.jpg)
 
 Test完的結果
 
 冬天變夏天:
 
 ![image](https://github.com/willy-lo/CVFX_HW1/blob/master/cv_hw1/test_after_before.png)
 
                         Before                                            After
                         
3.other method:
我們所使用的比較方式為利用Photoshop來將夏天的照片作成冬天的照片。 

首先我們將照片中綠色的飽和度降低，使照片中的草、樹、葉子等植物的樣貌看起來變枯萎，營造較沒有生氣盎然的感覺；同時將藍色的部份的飽和度也降低，因為冬天的天空會較為暗沉不會很藍。

接著選擇一個圖層(RGB、R、G、B任一個圖層皆可以)將其選擇之後，填入白色的成分，將這個圖層合成上去後，已經可以在些微地方看到白色如雪的成分。經過這些操作之後已經很有冬天的感覺了，且已經比使用cycleGAN 的效果更好了。

接下來仍然可以使照片更加完美，使用區塊將地板想要變成積雪的地方圈起來，填入白色之後添加適合的材質使得表面變的一點點粗糙讓他看似雪地。接著將圖片以白色的模糊效果使其增加霧氣感，最後再想要增加飄雪的地方使用筆刷刷出鏡頭前飄雪的感覺。

![image](https://github.com/willy-lo/CVFX_HW1/blob/master/cv_hw1/photoshop.jpg)

4.conclusion:

我們所採用的dataset是summer2winter,我們將train的epoch調整為150,decay epoch的參數調整為75。

一開始我們所採用的dataset不是summer2winter而是Monet2photo,但是因為Monet2photo的圖片太多了,以至於train的速度非常的緩慢,從第一題的進度條來看可能需要train到好幾天,所以我們這組就改掉dataset改用summer2winter。

把dataset改成summer2winter後,我們大概花了20個小時完成我們的training。之後我們丟了一張冬天的照片進去test,出來的結果我覺得效果沒有原本想像的可以完全變夏天的感覺,但是看得出來有像夏天了!

看完test的結果彷彿就像是新的夏天的照片多了一點點的雜訊(Moiré pattern莫列波紋)。做完這張後,我們也有把一張夏天的照片進去test去看他有沒有變成冬天的感覺,效果感覺也算是還不賴。


第三題用我們自己的方法,我們覺得夏天變冬天在photoshop可以做出很好的效果,我們利用調整參數的方式來完成,而夏天變冬天在test的結果並沒有比在photoshop來得好,我覺得Deep Learning的效果在夏天變冬天沒有比在photoshop來得好,所以我們覺得演算法方面還可以再更改一些,相信效果一定也可以變得更加好。而在冬天變夏天的部分,我們在photoshop幾乎很難做出來,因為把白色的東西變成彩色相對的是比較困難的,反而是在test上面我們呈現出來的效果我覺得還不錯,只是也是會有些雜訊。

以上是一些我們在這個dataset train跟test完分析的結果。



                         
 
 



