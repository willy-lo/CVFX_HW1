# CVFX_HW1
1.CycleGAN的原理:

CycleGAN的原理可以概述為：將一類圖片轉換成另一類圖片。也就是說，現在有兩個樣本空間，X和Y，我們希望把X空間中的樣本轉換成Y空間中的樣本。

因此，實際的目標就是學習從X到Y的映射。我們設這個映射為F。它就對應著GAN中的生成器，F可以將X中的圖片x轉換為Y中的圖片F(x)。對於生成的圖片，我們還需要GAN中的判別器來判別它是否為真實圖片，由此構成對抗生成網絡。設這個判別器為DY。這樣的話，根據這裡的生成器和判別器，我們就可以構造一個GAN損失，表達式為：

![image](https://github.com/willy-lo/CVFX_HW1/blob/master/cv_hw1/function1.png)

這個損失實際上和原始的GAN損失是一模一樣的。

但單純的使用這一個損失是無法進行訓練的。原因在於，映射F完全可以將所有x都映射為Y空間中的同一張圖片，使損失無效化。對此，有學者提出了所謂的“循環一致性損失”（cycle consistency loss）。

我們再假設一個映射G，它可以將Y空間中的圖片y轉換為X中的圖片G(y)。CycleGAN同時學習F和G兩個映射，並要求F(G(y)) ≈y，以及G(F(x)≈x 。也就是說，將X的圖片轉換到Y空間後，應該還可以轉換回來。這樣就杜絕模型把所有X的圖片都轉換為Y空間中的同一張圖片了。根據F(G(y)) ≈ y和G(F(x))≈ x，循環一致性損失就定義為：

![image](https://github.com/willy-lo/CVFX_HW1/blob/master/cv_hw1/function2.png)

同時，我們為G也引入一個判別器D_{X}，由此可以同樣定義一個GAN的損失LGAN(G,D_{X},X,Y)，最終的損失就由三部分組成：

![image](https://github.com/willy-lo/CVFX_HW1/blob/master/cv_hw1/function3.png)



CycleGAN與DCGAN的對比

為了進一步搞清楚CycleGAN的原理，我們可以拿它和其他幾個GAN模型，如DCGAN、pix2pix模型進行對比。


先來看下DCGAN，它的整體框架和最原始的那篇GAN是一模一樣的，在這個框架下，輸入是一個噪聲z，輸出是一張圖片（如下圖），因此，我們實際只能隨機生成圖片，沒有辦法控制輸出圖片的樣子，更不用說像CycleGAN一樣做圖片變換了。

![image](https://github.com/willy-lo/CVFX_HW1/blob/master/cv_hw1/pic1.png)



CycleGAN與pix2pix模型的對比



pix2pix也可以做圖像變換，它和CycleGAN的區別在於，pix2pix模型必須要求成對數據（paired data），而CycleGAN利用非成對數據也能進行訓練(unpaired data)。

![image](https://github.com/willy-lo/CVFX_HW1/blob/master/cv_hw1/pic2.png)

比如，我們希望訓練一個將白天的照片轉換為夜晚的模型。如果使用pix2pix模型，那麼我們必須在蒐集大量地點在白天和夜晚的兩張對應圖片，而使用CycleGAN只需同時蒐集白天的圖片和夜晚的圖片，不必滿足對應關係。因此CycleGAN的用途要比pix2pix更廣泛，利用CycleGAN就可以做出更多有趣的應用。



2.Training progress:  
 
  Monet2photo	
  
  剛開始train的進度條 :

![image](https://github.com/willy-lo/CVFX_HW1/blob/master/cv_hw1/monet2photo.png)

 Summer2winter	
 
 剛開始train的進度條:
 
![image](https://github.com/willy-lo/CVFX_HW1/blob/master/cv_hw1/summer2winter1.png)

 train到99%時的進度條:
 
 ![image](https://github.com/willy-lo/CVFX_HW1/blob/master/cv_hw1/summer2winter99.png)
 
3.test our pictures

 選取test的圖片

 ![image](https://github.com/willy-lo/CVFX_HW1/blob/master/cv_hw1/test_summer.jpg)
 
 Test完的結果
 
 夏天變冬天:
 
 ![image](https://github.com/willy-lo/CVFX_HW1/blob/master/cv_hw1/test_before_after.png)
                
                After                           Before
                          
 選取test的圖片      
 
 ![image](https://github.com/willy-lo/CVFX_HW1/blob/master/cv_hw1/test_winter.jpg)
 
 Test完的結果
 
 冬天變夏天:
 
 ![image](https://github.com/willy-lo/CVFX_HW1/blob/master/cv_hw1/test_after_before.png)
                        
               Before                            After
                         
4.other method:

我們所使用的比較方式為利用Photoshop來將夏天的照片作成冬天的照片。 

首先我們將照片中綠色的飽和度降低，使照片中的草、樹、葉子等植物的樣貌看起來變枯萎，營造較沒有生氣盎然的感覺；同時將藍色的部份的飽和度也降低，因為冬天的天空會較為暗沉不會很藍。

接著選擇一個圖層(RGB、R、G、B任一個圖層皆可以)將其選擇之後，填入白色的成分，將這個圖層合成上去後，已經可以在些微地方看到白色如雪的成分。經過這些操作之後已經很有冬天的感覺了，且已經比使用cycleGAN 的效果更好了。

接下來仍然可以使照片更加完美，使用區塊將地板想要變成積雪的地方圈起來，填入白色之後添加適合的材質使得表面變的一點點粗糙讓他看似雪地。接著將圖片以白色的模糊效果使其增加霧氣感，最後再想要增加飄雪的地方使用筆刷刷出鏡頭前飄雪的感覺。

![image](https://github.com/willy-lo/CVFX_HW1/blob/master/cv_hw1/photoshop.jpg)

5.conclusion:

我們所採用的dataset是summer2winter,我們將train的epoch調整為150,decay epoch的參數調整為75。

一開始我們所採用的dataset不是summer2winter而是Monet2photo,但是因為Monet2photo的圖片太多了,以至於train的速度非常的緩慢,從第一題的進度條來看可能需要train到好幾天,所以我們這組就改掉dataset改用summer2winter。

把dataset改成summer2winter後,我們大概花了20個小時完成我們的training。之後我們丟了一張冬天的照片進去test,出來的結果我覺得效果沒有原本想像的可以完全變夏天的感覺,但是看得出來有像夏天了!

看完test的結果彷彿就像是新的夏天的照片多了一點點的雜訊(Moiré pattern莫列波紋)。做完這張後,我們也有把一張夏天的照片進去test去看他有沒有變成冬天的感覺,效果感覺也算是還不賴。


第三題用我們自己的方法,我們覺得夏天變冬天在photoshop可以做出很好的效果,我們利用調整參數的方式來完成,而夏天變冬天在test的結果並沒有比在photoshop來得好,我覺得Deep Learning的效果在夏天變冬天沒有比在photoshop來得好,所以我們覺得演算法方面還可以再更改一些,相信效果一定也可以變得更加好。而在冬天變夏天的部分,我們在photoshop幾乎很難做出來,因為把白色的東西變成彩色相對的是比較困難的,反而是在test上面我們呈現出來的效果我覺得還不錯,只是也是會有些雜訊。

以上是一些我們在這個dataset train跟test完分析的結果。



                         
 
 



