/**
 * global variable : 비동기 로딩 이미지 사용여부
 * 비동기 로딩이미지를 사용하지 않을 경우, false로 설정할 것
 */
var ajaxLoadImgUse = true;

var App = (function($) {
	var init = function(option) {

		/* ajax start , end Method
		 */
		$(document).ajaxStart(function(e){
			if(ajaxLoadImgUse && $(".loading-dimed").length == 0) {
				loading_show();
			}
		});

		$(document).ajaxStop(function(){
			if($(".loading-dimed").length > 0) {
				loading_remove();
			}
			ajaxLoadImgUse = true;
		});

		// 비동기 로그인 요청
		$(document).ajaxError(function (event, xhr, thr){
			if(xhr.status == 401){
				alert('로그인이 필요합니다.');
				location.href="/login?returnUrl=" + encodeURI(location.pathname);
				return;
			} else {
				if(thr.url != "/inc/log") {
					alert('데이터 처리 도중 에러가 발생하였습니다.');
				}
			}
			ajaxLoadImgUse = true;
		});

		// vaildata alter 변경
		$.extend( $.validator.defaults, {
			 invalidHandler: function(form, validator) {
				var errors = validator.numberOfInvalids();
				if (errors) {
					alert(validator.errorList[0].message);
					var errEle = validator.errorList[0].element;
					// CK EDITOR 경우
					if($(errEle).prop("tagName")=="TEXTAREA" && $(errEle).next().hasClass("cke")) {
						CKEDITOR.instances[$(errEle).next().attr("id").replace("cke_","")].focus();
					// FILE 경우
					//} else if ($(errEle).attr('type') === "file" && $(errEle).data('style') === "fileinput"){
					//	$(validator.errorList[0].element).click();
					} else {
						validator.errorList[0].element.focus();
					}
				}
			},
			ignore: [], // CKEDITOR가 텍스트 영역을 숨기므로 jQuery 유효성 검사는 요소의 유효성을 검사하지 않습니다.
			onkeyup:false,
			onfocusout:false,
		    showErrors:function(errorMap, errorList){
	            /*if(this.numberOfInvalids()) { // 에러가 있을 때만..
	                alert(errorList[0].message);
	                $(errorList[0].element).focus()
	            }*/
	        },
			errorPlacement: function(error, element) {
				/*if (element.attr('type') === "file" && element.data('style') === "fileinput"){
					error.appendTo(element.closest("div.fileinput-holder").parent('div'));
				} else if (element.data('parent_class')) {
					error.appendTo(element.parents('.'+element.data('parent_class')));
				} else {
					error.insertAfter(element)
				}*/
			}
		});

	};

	return {
		init: init
	};
}(jQuery));

/**
 * vaildator 공백 처리
 * */
(function ($) {
    $.each($.validator.methods, function (key, value) {
        $.validator.methods[key] = function () {
            if(arguments.length > 0) {
                arguments[0] = $.trim(arguments[0]);
            }

            return value.apply(this, arguments);
        };
    });
} (jQuery));


/**
 * 전역함수
 **/
//loading
function loading_show(){
	$('body').append('<div class="loading-dimed"></div>');

}
function loading_remove(){
	$('.loading-dimed').remove();
	/*setTimeout(function(){
		$(".ellipsis-muti").ellipsis();
		UI.customScroll.scrollY($('.perform-wrap.scroll-y'));
	},500);*/
}
// 일시포맷
function formatDate(date, format) {
	if(!format) {
		format = 'YYYY-MM-DD';
	}
	return (date ? moment(date).format(format) : '');
}
// 레이어팝업 오픈
function openPopup(options) {
	if (options.event) {
		event.preventDefault()
	}
	$('body').append('<div id="popup_result" style="z-index: 10;"/>');
	$('html, body').addClass('body_hidden');
	//$('#popup_result').load(options.url + ' #popup_layer');
	$('#popup_result').load(options.url);
	if (options.callback) {
		$('#popup_result').data('callback', options.callback);
	}
}
//레이어팝업 클로즈
function closePopup(event) {
	if (event) {
		event.preventDefault();
	}
	$('#popup_result').remove();
	$('html, body').removeClass('body_hidden');
}
// 함수이름으로 함수정의 얻기
function getFunctionByNm(nm) {
	if (!nm || !nm.split('.')) {
		return null;
	}
	var ret = window;
	nm.split('.').forEach(function(item, index) {
		ret = ret[item];
	});

	if (!ret || typeof ret !== 'function') {
		return null;
	}
	return ret;
};
// 이미지업로드
function uploadImage($form, $file, callback, callbackOptions) {
	if (!$file || !$file.val()) {
		return false;
	}

	var orgNm = $file.attr('name');
	$file.attr('name', 'atchFile')

	$form.ajaxSubmit({
		type: 'post', dataType: 'json',
		url: '/upload/image',
		success: function(data) {
			$file.attr('name', orgNm);
			$file.val('');

			if (data && typeof data !== 'object') {
				data = $.parseJSON(data);
			}
			if (data && data.result === 'success') {
				// 업로드 후처리
				if (typeof callback === 'function')
					callback(data, callbackOptions);

			} else {
				if (data && data.message) {
					alert(data.message);
					return false;
				} else {
					alert('데이터 처리 도중 에러가 발생하였습니다');
					return false;
				}
			}
		}
	});
}
//파일업로드
function uploadFile($form, $file, callback) {
	if (!$file || !$file.val()) {
		return false;
	}

	var orgNm = $file.attr('name');
	$file.attr('name', 'atchFile')

	$form.ajaxSubmit({
		type: 'post', dataType: 'json',
		url: '/upload/file',
		success: function(data) {
			$file.attr('name', orgNm);
			$file.val('');

			if (data && typeof data !== 'object') {
				data = $.parseJSON(data);
			}
			if (data && data.result === 'success') {
				// 업로드 후처리
				if (typeof callback === 'function')
					callback(data);

			} else {
				if (data && data.message) {
					alert(data.message);
					return false;
				} else {
					alert('데이터 처리 도중 에러가 발생하였습니다');
					return false;
				}
			}
		}
	});
}

function showLength() {
	$('input[type="text"].txtMaxlen').each(function(item) {
		var $txtMaxlen = $(this);
		// span 초기화
		$txtMaxlen.next('.lbMaxlen').remove();

		// span 추가
        var maxlen = $txtMaxlen.attr('maxlength');
        var len = $txtMaxlen.val().length;
        $txtMaxlen.after('<span class="lbMaxlen">' + len + '/' + maxlen +'</span>');

        // bind event : change
        $txtMaxlen.off('keyup').on('keyup', function() {
			var $this = $(this);

			// span 초기화
			$this.next('.lbMaxlen').remove();

			// span 추가
            var maxlen = $this.attr('maxlength');
            var len = $this.val().length;
            $this.after('<span class="lbMaxlen">' + len + '/' + maxlen +'</span>');


        });
	});

	$('textarea.txtMaxlen').each(function(item) {
		var $txtMaxlen = $(this);
		// span 초기화
		$txtMaxlen.next('.lbMaxlen_textarea').remove();

		// span 추가
        var maxlen = $txtMaxlen.attr('maxlength');
        var len = $txtMaxlen.val().length;
        $txtMaxlen.after('<span class="lbMaxlen_textarea">' + len + '/' + maxlen +'</span>');

        // bind event : change
        $txtMaxlen.off('keyup').on('keyup', function() {
			var $this = $(this);

			// span 초기화
			$this.next('.lbMaxlen_textarea').remove();

			// span 추가
            var maxlen = $this.attr('maxlength');
            var len = $this.val().length;
            $this.after('<span class="lbMaxlen_textarea">' + len + '/' + maxlen +'</span>');


        });
	});
}

// 로그인아이디 포맷체크
function checkLoginIdFormat(value) {
	var check = /^[A-Za-z0-9]{5,20}$/;
	return check.test(value);
}
// 로그인비밀번호 포맷체크
function checkPasswordFormat(value) {
	if (value.length < 8 || value.length > 20)
		return false;

	var check = /(?=.*[0-9])(?=.*[a-zA-Z])(?=.*[^a-zA-Z0-9]).{8,20}$/;
	return check.test(value);
}
