# envi_idl_experience

因为比赛了解了一下这个语言，idl，太冷门了，教程太少，还不完善，5.1以后还不支持可视化GUI设计

```
# main
pro main ,INPUT=input, OUTPUT=output

outf_base=widget_base(base,yOffset=210)
outf = WIDGET_OUTFM(outf_base, uvalue='outf', /frame)//输出控件
  
  
ok = WIDGET_BUTTON(base, value = 'OK', uname = 'ok',xOffset=150,yOffset=350)//ok按钮控件

class_base=widget_base(base,xOffset=30,yOffset=10)
class_list=['oli','etm','tm']
class=widget_menu(class_base,List=class_list,/EXCLUSIVE)//单选控件

pState = {text_1:text_1,text_2:text_2,text_3:text_3,class:class,outf:outf}
WIDGET_CONTROL, base, set_uvalue = pState//传递参数的方法，绑定在base里面
  
end  
```


```
#base_event//函数
pro base_event,ev

WIDGET_CONTROL, ev.TOP, get_uvalue = pState//获取参数传递
text_1=pState.text_1
outf=pState.outf
class=pState.class

CASE WIDGET_INFO(ev.ID, /uname) OF
    'ok': BEGIN
      WIDGET_CONTROL,text_1,get_value=t1     
      widget_control,class,get_value=selected
      widget_control,outf,get_value=address
      if (selected eq -1) then return     
    end
    else:
  endcase
end
```
