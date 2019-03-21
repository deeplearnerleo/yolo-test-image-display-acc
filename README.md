# yolo-test-image-display-acc
darknet 网络里更改，显示准确率
首先打开darknet/src配置文件中找到image.c文件
然后在image.c文件中找到draw_detections函数，加入一下代码
void draw_detections(image im, detection *dets, int num, float thresh, char **names, image **alphabet, int classes)
{
    int i,j;

    for(i = 0; i < num; ++i){
        char labelstr[4096] = {0};
        int class = -1;
        for(j = 0; j < classes; ++j){
        
        char res[20]={0};
       
            if (dets[i].prob[j] > thresh){
                if (class < 0) {
                    strcat(labelstr, names[j]);
                    class = j;
                } else {
                    strcat(labelstr, ", ");
                    strcat(labelstr, names[j]);
                }
                sprintf(res,"%.2f",dets[i].prob[j]*100);
                strcat(labelstr,":")
                strcat(labelstr,res)
                strcat(labelstr,"%")
                printf("%s: %.0f%%\n", names[j], dets[i].prob[j]*100);
            }
        }
