
## MouseScrollToLeft - 鼠标滚轮横向移动(无滚动条）
  鼠标放在页面上滚动鼠标滚轮，页面会横向移动，而不是竖向移动

## 代码
>class MouseScrollToLeft {  
>>constructor(obj, father) {  
>>>this.obj = obj  
>>>this.father = father  
>>}  
    init() {  
      this.obj.style.left = '0px'  
      this.father.style.overflow = 'hidden'  
      this.father.addEventListener("wheel", (e) => this.mouseScroll(e), false)  
    }  
    mouseScroll(e = window.event) {  
      // wheelDelta ie 谷歌; detail 火狐  
      const key = e.wheelDelta ? 'wheelDelta' : (e.detail ? 'detail' : '')  

      const num = Number(this.obj.style.left.split('p')[0]) + e[key] / 2  
      this.obj.style.left = num > 0 || Math.abs(num) > this.father.clientWidth ? this.obj.style.left : num + 'px'  

      // 左边触底 归0  
      this.obj.style.left = num >= 0 ? 0 : this.obj.style.left  

      // 右边触底 left 为obj宽度和father宽度差值  
      this.obj.style.left = Math.abs(num) >= this.obj.clientWidth - this.father.clientWidth ?  
        this.father.clientWidth - this.obj.clientWidth + 'px' :  
        this.obj.style.left  
    }  
  }  

## 用法
  obj为DOM对象，father为obj的父级元素  
  const ToLeft = new MouseScrollToLeft(obj, father).init()
