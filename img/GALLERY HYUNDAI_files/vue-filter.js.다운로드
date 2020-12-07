/** Vue 값 콤마 처리 **/
Vue.filter('numberWithCommas' , function (value){
	return numberWithCommas(value);
});
/** Vue 날짜 타입 변경. **/
Vue.filter('timeToDate' , function (stmp, returnType){
	var str = formatDate(stmp, returnType);
	if (!str) {
		return null;
	} else {
		return str.toUpperCase();
	}
});
/** yyyymmdd to yyyy년 mm월 **/
Vue.filter('yyyymmToStr' , function (value){

	if (!value) return '';
	value = value.toString();
	return value.substring(0,4) + "년 " + value.substring(4,6) + "월";

});
/** replace return to <br> **/
Vue.filter('returnToBr' , function (value) {
	if (!value) return '';
	return value.replace(/(\n|\r\n)/g, '<br>');
});
Vue.filter('formatExbiPlace', function(exbiPlaceList) {
	if (!exbiPlaceList || exbiPlaceList.length < 1) {
		return '';
	}
	var ret = '';
	exbiPlaceList.forEach(function(item, index) {
		if (ret) ret += ', ';
		ret += item.exbiPlaceNm;
	});
	return ret;
});
Vue.filter('formatExbiPeriod', function(exbi) {
	// Sep 24 – Oct 31, 2019
	var ret = '';
	if (!exbi.beginDt || !exbi.endDt) return ret;

	if (formatDate(exbi.beginDt, 'YYYY') === formatDate(exbi.endDt, 'YYYY')) {
		ret = formatDate(exbi.beginDt, 'MMM D') + ' – ' +
				formatDate(exbi.endDt, 'MMM D, YYYY');
	} else {
		ret = formatDate(exbi.beginDt, 'MMM D, YYYY') + ' – ' +
				formatDate(exbi.endDt, 'MMM D, YYYY');
	}
	return ret;
});
Vue.filter('formatArtfairPlace', function(artfairPlaceList) {
	if (!artfairPlaceList || artfairPlaceList.length < 1) {
		return '';
	}
	var ret = '';
	artfairPlaceList.forEach(function(item, index) {
		if (ret) ret += ', ';
		ret += item.artfairPlaceNm;
	});
	return ret;
});
Vue.filter('formatArtfairPeriod', function(artfair) {
	// Sep 24 – Oct 31, 2019
	var ret = '';
	if (!artfair.beginDt || !artfair.endDt) return ret;

	if (formatDate(artfair.beginDt, 'YYYY') === formatDate(artfair.endDt, 'YYYY')) {
		ret = formatDate(artfair.beginDt, 'MMM D') + ' – ' +
				formatDate(artfair.endDt, 'MMM D, YYYY');
	} else {
		ret = formatDate(artfair.beginDt, 'MMM D, YYYY') + ' – ' +
				formatDate(artfair.endDt, 'MMM D, YYYY');
	}
	return ret;
});
