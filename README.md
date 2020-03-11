```js

function why_i_hate_code(){

    // its so simple and does just what we need
    // wow, beautiful...
    mobile_menu = function(){
        $('body').on('click', '.mobile-menu-trigger', function(){
            $('mobile-menu').toggleClass('active');
        });
    };

    // well, web browsers are kind of trash. I better let the body
    // tag know if the menu is open or not.    
    mobile_menu = function(){

        var body = $('body');

        body.on('click', '.mobile-menu-trigger', function(){

            var m = $('mobile-menu');

            m.toggleClass('active');

            if ( m.hasClass('active') ){
                body.addClass('mobile-menu-active');
            } else {
                body.removeClass('mobile-menu-active');
            }
        });
    };

    // I knew I was going to have to do this, but...
    // if no close buttons are visible on the page, we have to
    // close the menu automatically.
    // better wrap everything into stupid little functions.
    mobile_menu = function(){

        var body = $('body');
        var menu = $('.mobile-menu');

        function open(){
            menu.addClass('active');
            body.addClass('mobile-menu-active');
        }

        function close(){
            menu.removeClass('active');
            body.removeClass('mobile-menu-active');
        }

        function is_open(){
            return menu.hasClass('active');
        }

        function toggle(){
            if ( is_open() ) {
                close();
            } else{
                open();
            }
        }

        function any_triggers_visible(){
            return $('.mobile-menu-trigger:visible').length > 0;
        }

        $('window').on('resize', function(){
            if ( ! any_triggers_visible() ) {
                close();
            }
        });

        body.on('click', '.mobile-menu-trigger', function(){
            toggle();
        });

    };

    // FINE, FUCK IT
    mobile_menu = function( init ){

        var self = {};

        self.body = $('body');
        self.menu = $('.mobile-menu');

        self.open = function(){
            self.menu.addClass('active');
            self.body.addClass('mobile-menu-active');
        };

        self.close = function(){
            self.menu.removeClass('active');
            self.body.removeClass('mobile-menu-active');
        };

        self.is_open = function(){
            return self.menu.hasClass('active');
        };

        self.toggle = function(){
            if ( self.is_open() ) {
                self.close();
            } else{
                self.open();
            }
        };

        self.any_triggers_visible = function(){
            return $('.mobile-menu-trigger:visible').length > 0;
        };

        self.init = function(){

            $('window').on('resize', function(){
                if ( ! self.any_triggers_visible() ) {
                    self.close();
                }
            });

            self.body.on('click', '.mobile-menu-trigger', function(){
                self.toggle();
            });
        };

        if ( init ) {
            self.init();
        }

        return self;
    };

}

```
