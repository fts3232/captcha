# captcha
[![Latest Stable Version](https://poser.pugx.org/fts/captcha/v/stable)](https://packagist.org/packages/fts/captcha)
[![Total Downloads](https://poser.pugx.org/fts/captcha/downloads)](https://packagist.org/packages/fts/captcha)
[![License](https://poser.pugx.org/fts/captcha/license)](https://packagist.org/packages/fts/captcha)

# 功能
* 生成验证码
* 检查验证码
# 安装
    composer require fts/captcha
### 发布配置文件
     php artisan vendor:publish
### 添加服务提供者
打开 `config/app.php` 并添加以下内容到 providers 数组:
    
    fts\CaptchaServiceProvider.php::class
# 用法
     Route::any('captcha-test', function()
        {
            if (Request::getMethod() == 'POST')
            {
                $rules = ['captcha' => 'required|captcha'];
                $validator = Validator::make(Input::all(), $rules);
                if ($validator->fails())
                {
                    echo '<p style="color: #ff0000;">Incorrect!</p>';
                }
                else
                {
                    echo '<p style="color: #00ff30;">Matched :)</p>';
                }
            }
        
            $form = '<form method="post" action="captcha-test">';
            $form .= '<input type="hidden" name="_token" value="' . csrf_token() . '">';
            $form .= '<p>' . captcha_img() . '</p>';
            $form .= '<p><input type="text" name="captcha"></p>';
            $form .= '<p><button type="submit" name="check">Check</button></p>';
            $form .= '</form>';
            return $form;
        });
### 获取图片
    captcha();
### 获取图片html
    captcha_src();
### 获取图片url
    captcha_img();