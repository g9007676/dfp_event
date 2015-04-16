# dfp_event

最近有個需求需要在 dfp 上綁定事件，看到有人寫的 js 就記錄一下。

作者repot:https://github.com/mcountis/dfp-events

# Demo

    googletag.cmd.push(function() { googletag.display('div-gpt-ad-1424913848854-0');    
        //callback method
        googletag.on('gpt-slot_rendered',function(e,level,message,service,slot,reference){
        var slotId = slot.getSlotId(),
        slot = $('#'+slotId.getDomId());
        
        if(slot.find('iframe:not([id*=hidden])')
            .map(function () { return this.contentWindow.document; })
            .find('body')
            .children().length != 0
        ){
            var slot_img = slot.find('iframe').contents().find('img');
            console.log(slot_img);
            slot_img.bind('touchmove', function (e) {     
                var nowY = e.originalEvent.touches ? e.originalEvent.touches[0].pageY : e.pageY;                    
                console.log('touchmove');
            });
            slot_img.bind('touchstart', function (e) {
                startY = e.originalEvent.touches ? e.originalEvent.touches[0].pageY : e.pageY;                           
            }).bind('touchend', function (e) {              
                var nowY = e.originalEvent.changedTouches ? e.originalEvent.changedTouches[0].pageY : e.pageY; 
                console.log(123);                                                                      
                if (startY > nowY) {
                    $('h1 .tabbar').animate({top:'40px'},300);
                    $('h1').animate({height:'100px'},300);
                    return ;
                }
                $('h1 .tabbar').animate({top:'-50px'},300);
                $('h1').animate({height:'40px'},300);
            });
            $('h1 .tabbar').css({top:'40px'});
            $('h1').css({height:'100px'});
            } 
        });
    });
