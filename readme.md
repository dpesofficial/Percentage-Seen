var $element = $('#element');
var $win = $(window);
var $vis = $('#visible');

$win.on('scroll', function () {
    console.log(percentageSeen());
    $vis.text(percentageSeen() + '%');
});

function percentageSeen () {
    var viewportHeight = $(window).height(),
        scrollTop = $win.scrollTop(),
        elementOffsetTop = $element.offset().top,
        elementHeight = $element.height();


    if (elementOffsetTop > (scrollTop + viewportHeight)) {
        return 0;
    } else if ((elementOffsetTop + elementHeight) < scrollTop) {
        return 100;
    } else {
        var distance = (scrollTop + viewportHeight) - elementOffsetTop;
        var percentage = distance / ((viewportHeight + elementHeight) / 100);
        percentage = Math.round(percentage);
        return percentage;
    }
}

$win.trigger('scroll');
