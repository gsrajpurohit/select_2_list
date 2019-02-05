/*!
 * Select to List jQuery Plugin - v1.0.0-beta1
 *
 * Copyright 2017 Ganpat S Rajpurohit, Jaipur.
 *
 * Licensed MIT
 */
if (typeof Object.create !== 'function') {
    Object.create = function(obj) {
        function F() {}
        F.prototype = obj;
        return new F();
    };
}

(function($, window, document, undefined) {
    $.strip_tags = function(value) {
        var body = value || '';
        var regex = /(<([^>]+)>)/ig;
        return body.replace(regex, "");
    }
    var SELECT_2_LIST = {
        /*!
         * Initialize the plugin.
         *
         * @param DOM element.
         * @param Object options The plugin instance settings.
         */
        _init: function(el, options) {
            var self = this;
            this.settings = $.extend({}, $.fn.select_2_list.defaults, options);
            this.$el = $(el);
            this.selectedValues = [];
            var settings = this.settings;
            $(el).each(function() {
                self._createList();
                self._addHandler();
                self._addEvents();
            })
        },
        init: function() {
            this._init.call(this, this.$el, this.settings);
        },
        _createList: function() {
            var self = this;
            var settings = self.settings;
            var $list = $('<ul />', {
                'class': 'dd-list',
                'style': 'max-height: '+settings.max_height+'px; overflow-y: auto;'
            });

            var $item = $('<li />', {
                    'class': 'dd-item',
                    'value': '',
                })
                .text(settings.selected_text);
            $list.append($item);
            $('option', self.$el).each(function(index, el) {
                var value = $(this).val(),
                    text = $(this).text();
                if(value != '') {
                    var $item = $('<li />', {
                            'class': 'dd-item',
                            'value': value,
                        })
                        .text(text);
                    $list.append($item);
                }
            });
            self.$wrapper = self.$el.parent();
            self.$list = $list;
            self.$el.parent().addClass('dd-list-wrapper').html($list);
        },
        _addHandler: function() {
            var self = this;
            var settings = self.settings;
            var $handler = $('<span />', {
                    'class': 'dd-list-handler',
                })
                .text(settings.selected_text);
            self.$handler = $handler;
            self.$wrapper.prepend($handler);
        },
        _addEvents: function() {
            var self = this;
            var $el = self.$el;
            var settings = self.settings;
            self.$handler.on('click', function(event) {
                event.preventDefault();
                self.$list.slideToggle(settings.easing_time);
                self.$wrapper.data('list', self.$list);
                self.$list.data('wrapper', self.$wrapper);
            });

            $('ul li', self.$wrapper).on('click', function(event) {
                event.preventDefault();
                var text = $(this).text(),
                    value = self.selectedValues = $(this).attr('value');
                $('ul li', self.$wrapper).removeClass('active');
                $(this).addClass('active');
                self.$handler.text(text).data('value', value);
                self.$list.slideUp(settings.easing_time);
                self.settings.onSelect.call(self, self.selectedValues);
            });


            self._hideList();
        },
        _hideList: function() {
            var self = this;
            var el = self.$el;
            var settings = self.settings;

            $(document).on('click', function(e) {
                self.$wrapper.each(function() {
                    // var $ul = $(this).find('ul');
                    if (!$(this).is(e.target) && $(this).has(e.target).length === 0 && self.$list.has(e.target).length === 0) {
                        self.$list.slideUp(settings.easing_time);
                    }
                });
            });
        },
        getSelectedValues: function() {
            return this.selectedValues;
        },
    }

    $.fn.select_2_list = function(options) {
        if ($.isPlainObject(options)) {
            return this.each(function() {
                var select_2_list = Object.create(SELECT_2_LIST);
                select_2_list._init(this, options);
                $(this).data('select_2_list', select_2_list);
            });
        } else if (typeof options === 'string' && options.indexOf('_') !== 0) {
            var select_2_list = $(this).data('select_2_list');
            var method = select_2_list[options];
            return method.apply(select_2_list, $.makeArray(arguments).slice(1));
        }
    };

    $.fn.select_2_list.defaults = {
        easing_out: 500,
        max_height: 100,
        selected_text: 'Select',
        onSelect: function() { return true; }
    };

})(jQuery, window, document);
