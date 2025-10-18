<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>账号登录</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', 'Microsoft YaHei', sans-serif;
        }
        
        body {
            background: linear-gradient(135deg, #6a11cb 0%, #2575fc 100%);
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            padding: 20px;
        }
        
        .login-container {
            background-color: white;
            border-radius: 12px;
            box-shadow: 0 15px 30px rgba(0, 0, 0, 0.2);
            width: 100%;
            max-width: 420px;
            padding: 40px 30px;
            transition: transform 0.3s ease;
        }
        
        .login-container:hover {
            transform: translateY(-5px);
        }
        
        .login-header {
            text-align: center;
            margin-bottom: 30px;
        }
        
        .login-header h1 {
            color: #333;
            font-size: 28px;
            font-weight: 600;
            margin-bottom: 8px;
        }
        
        .login-header p {
            color: #666;
            font-size: 14px;
        }
        
        .form-group {
            margin-bottom: 20px;
            position: relative;
        }
        
        .form-group label {
            display: block;
            margin-bottom: 8px;
            color: #555;
            font-size: 14px;
            font-weight: 500;
        }
        
        .input-with-icon {
            position: relative;
        }
        
        .input-with-icon i {
            position: absolute;
            left: 15px;
            top: 50%;
            transform: translateY(-50%);
            color: #999;
        }
        
        .form-control {
            width: 100%;
            padding: 14px 15px 14px 45px;
            border: 1px solid #ddd;
            border-radius: 8px;
            font-size: 16px;
            transition: all 0.3s;
        }
        
        .form-control:focus {
            border-color: #4a7dff;
            box-shadow: 0 0 0 2px rgba(74, 125, 255, 0.2);
            outline: none;
        }
        
        .password-toggle {
            position: absolute;
            right: 15px;
            top: 50%;
            transform: translateY(-50%);
            background: none;
            border: none;
            color: #999;
            cursor: pointer;
        }
        
        .options {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 25px;
            font-size: 14px;
        }
        
        .remember-me {
            display: flex;
            align-items: center;
        }
        
        .remember-me input {
            margin-right: 8px;
        }
        
        .forgot-password {
            color: #4a7dff;
            text-decoration: none;
            transition: color 0.2s;
        }
        
        .forgot-password:hover {
            color: #2c5fd1;
            text-decoration: underline;
        }
        
        .login-btn {
            width: 100%;
            padding: 14px;
            background: linear-gradient(135deg, #6a11cb 0%, #2575fc 100%);
            color: white;
            border: none;
            border-radius: 8px;
            font-size: 16px;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s;
        }
        
        .login-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(74, 125, 255, 0.4);
        }
        
        .login-btn:active {
            transform: translateY(0);
        }
        
        .divider {
            display: flex;
            align-items: center;
            margin: 25px 0;
        }
        
        .divider::before,
        .divider::after {
            content: "";
            flex: 1;
            height: 1px;
            background-color: #eee;
        }
        
        .divider span {
            padding: 0 15px;
            color: #999;
            font-size: 14px;
        }
        
        .social-login {
            display: flex;
            justify-content: center;
            gap: 15px;
            margin-bottom: 25px;
        }
        
        .social-btn {
            width: 45px;
            height: 45px;
            border-radius: 50%;
            display: flex;
            justify-content: center;
            align-items: center;
            border: 1px solid #ddd;
            background: white;
            cursor: pointer;
            transition: all 0.3s;
        }
        
        .social-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 5px 10px rgba(0, 0, 0, 0.1);
        }
        
        .social-btn i {
            font-size: 18px;
        }
        
        .wechat {
            color: #09bb07;
        }
        
        .qq {
            color: #12b7f5;
        }
        
        .weibo {
            color: #e6162d;
        }
        
        .register-link {
            text-align: center;
            font-size: 14px;
            color: #666;
        }
        
        .register-link a {
            color: #4a7dff;
            text-decoration: none;
            font-weight: 500;
            margin-left: 5px;
        }
        
        .register-link a:hover {
            text-decoration: underline;
        }
        
        .error-message {
            color: #e74c3c;
            font-size: 13px;
            margin-top: 5px;
            display: none;
        }
        
        @media (max-width: 480px) {
            .login-container {
                padding: 30px 20px;
            }
            
            .options {
                flex-direction: column;
                align-items: flex-start;
                gap: 10px;
            }
        }
    </style>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css">
</head>
<body>
    <div class="login-container">
        <div class="login-header">
            <h1>欢迎回来</h1>
            <p>请输入您的账号和密码进行登录</p>
        </div>
        
        <form id="loginForm">
            <div class="form-group">
                <label for="username">用户名 / 邮箱 / 手机号</label>
                <div class="input-with-icon">
                    <i class="fas fa-user"></i>
                    <input type="text" id="username" class="form-control" placeholder="请输入用户名、邮箱或手机号" required>
                </div>
                <div class="error-message" id="username-error">请输入有效的用户名、邮箱或手机号</div>
            </div>
            
            <div class="form-group">
                <label for="password">密码</label>
                <div class="input-with-icon">
                    <i class="fas fa-lock"></i>
                    <input type="password" id="password" class="form-control" placeholder="请输入密码" required>
                    <button type="button" class="password-toggle" id="togglePassword">
                        <i class="fas fa-eye"></i>
                    </button>
                </div>
                <div class="error-message" id="password-error">密码不能少于6个字符</div>
            </div>
            
            <div class="options">
                <div class="remember-me">
                    <input type="checkbox" id="remember">
                    <label for="remember">记住我</label>
                </div>
                <a href="#" class="forgot-password">忘记密码?</a>
            </div>
            
            <button type="submit" class="login-btn">登录</button>
        </form>
        
        <div class="divider">
            <span>或使用以下方式登录</span>
        </div>
        
        <div class="social-login">
            <div class="social-btn wechat">
                <i class="fab fa-weixin"></i>
            </div>
            <div class="social-btn qq">
                <i class="fab fa-qq"></i>
            </div>
            <div class="social-btn weibo">
                <i class="fab fa-weibo"></i>
            </div>
        </div>
        
        <div class="register-link">
            还没有账号? <a href="#">立即注册</a>
        </div>
    </div>

    <script>
        document.addEventListener('DOMContentLoaded', function() {
            const loginForm = document.getElementById('loginForm');
            const togglePassword = document.getElementById('togglePassword');
            const passwordInput = document.getElementById('password');
            const usernameInput = document.getElementById('username');
            const usernameError = document.getElementById('username-error');
            const passwordError = document.getElementById('password-error');
            
            // 切换密码可见性
            togglePassword.addEventListener('click', function() {
                const type = passwordInput.getAttribute('type') === 'password' ? 'text' : 'password';
                passwordInput.setAttribute('type', type);
                this.innerHTML = type === 'password' ? '<i class="fas fa-eye"></i>' : '<i class="fas fa-eye-slash"></i>';
            });
            
            // 表单验证
            loginForm.addEventListener('submit', function(e) {
                e.preventDefault();
                let isValid = true;
                
                // 验证用户名
                if (usernameInput.value.trim() === '') {
                    usernameError.style.display = 'block';
                    usernameInput.style.borderColor = '#e74c3c';
                    isValid = false;
                } else {
                    usernameError.style.display = 'none';
                    usernameInput.style.borderColor = '#ddd';
                }
                
                // 验证密码
                if (passwordInput.value.length < 6) {
                    passwordError.style.display = 'block';
                    passwordInput.style.borderColor = '#e74c3c';
                    isValid = false;
                } else {
                    passwordError.style.display = 'none';
                    passwordInput.style.borderColor = '#ddd';
                }
                
                // 如果验证通过，模拟登录
                if (isValid) {
                    const loginBtn = document.querySelector('.login-btn');
                    loginBtn.innerHTML = '<i class="fas fa-spinner fa-spin"></i> 登录中...';
                    loginBtn.disabled = true;
                    
                    // 模拟API请求
                    setTimeout(() => {
                        alert('登录成功！');
                        loginBtn.innerHTML = '登录';
                        loginBtn.disabled = false;
                    }, 1500);
                }
            });
            
            // 输入时实时验证
            usernameInput.addEventListener('input', function() {
                if (this.value.trim() !== '') {
                    usernameError.style.display = 'none';
                    this.style.borderColor = '#ddd';
                }
            });
            
            passwordInput.addEventListener('input', function() {
                if (this.value.length >= 6) {
                    passwordError.style.display = 'none';
                    this.style.borderColor = '#ddd';
                }
            });
        });
    </script>
</body>
</html>
