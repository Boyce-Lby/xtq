var Script = function () {


//    tool tips

    $('.tooltips').tooltip();

//    popovers

    $('.popovers').popover();

//    bxslider

    // $('.bxslider').show();
    // $('.bxslider').bxSlider({
    //     minSlides: 4,
    //     maxSlides: 4,
    //     slideWidth: 276,
    //     slideMargin: 20
    // });

}();

	(function() {

   			$('<i id="back-to-top"></i>').appendTo($('body'));

			$(window).scroll(function() {

				if($(this).scrollTop() != 0) {
					$('#back-to-top').fadeIn();	
				} else {
					$('#back-to-top').fadeOut();
				}

			});
			
			$('#back-to-top').click(function() {
				$('body,html').animate({scrollTop:0},600);
			});	

	})();

//以下为修改jQuery Validation插件兼容Bootstrap的方法，没有直接写在插件中是为了便于插件升级
        $.validator.setDefaults({
            highlight: function (element) {
                $(element).closest('.form-group').removeClass('has-success').addClass('has-error');
            },
            success: function (element) {
                element.closest('.form-group').removeClass('has-error').addClass('has-success');
            },
            errorElement: "span",
            errorPlacement: function (error, element) {
                if (element.is(":radio") || element.is(":checkbox")) {
                    error.appendTo(element.parent().parent().parent());
                } else {
                    error.appendTo(element.parent());
                }
            },
            errorClass: "help-block m-b-none",
            validClass: "help-block m-b-none"


		});
/**
 * 实时校验手机号是否已经注册
 */
function checkMobile() {
	var mobile = $("#mobile").val();
	$("#mobileMsg").html("");
	var con = false;
	if (mobile == "") {
		$("#mobileMsg").html("&nbsp;&nbsp;&nbsp;&nbsp;*手机号码不能为空");
	} else {
		// 手机号码不为空
		$.ajax({
			type : 'GET',
			async:false,
			url : 'http://passport.xtq993.com/validateMobile.htm?mobile=' + mobile,
			success : function(data) {
				if(data.code ==10102){
					$("#mobileMsg").html("*不是有效手机号码");
				}else if(data.code==10101){
					$("#mobileMsg").html("*手机号码不能为空");
				}else if(data.code==10104){//校验通过
					con = true;
				}else if(data.code==10103){
					$("#mobileMsg").html("*手机号已注册");
				}else{
					layer.msg('系统错误');
				}
			}
		});
	}
	return con;
};
/**
 * 发送手机验证码
 */
function sendCode() {
	var value = $("#mobile").val();
	var _this = $("#send");
	$("#codeMsg").html("");
	//点击后直接禁用，并开始计时
	_this.attr("disabled", "true");
	var countdown = 60;
	//设置button效果，开始计时  
	_this.html(countdown + "秒后重新获取");
	//启动计时器，1秒执行一次  
	var timer = setInterval(function() {
		if (countdown == 0) {
			clearInterval(timer);//停止计时器  
			_this.removeAttr("disabled");//启用按钮  
			_this.html("重新发送验证码");
		} else {
			countdown--;
			_this.html(countdown + "秒后重新获取");
		}
	}, 1000);
	$.ajax({
		type : 'GET',
		url : 'http://passport.xtq993.com/verificationCode.htm?type=mobile&mobile=' + value,
		success : function(data) {
			if(data.code==10101){
				$("#codeMsg").html("*手机号不能为空");
			}else if(data.code==10102){
				$("#codeMsg").html("*不是有效的手机号码");
			}else if(data.code==10000){//发送成功
			}else if(data.code==90000){
				$("#codeMsg").html("*短信发送超时，请稍后再试");
			}else{
				layer.msg('系统错误');
			}
		}
	});
}
