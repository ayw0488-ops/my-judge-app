[index.html](https://github.com/user-attachments/files/24987020/index.html)
<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>로그인 - 내탓네탓</title>
    <style>
        /* 기존 스타일 유지 */
        body { margin: 0; background-color: #ffffff; font-family: 'Pretendard', sans-serif; color: #333333; }
        .mobile-container {
            width: 100%; max-width: 430px; min-height: 100vh; margin: 0 auto;
            display: flex; flex-direction: column; align-items: center; justify-content: center;
            padding: 40px; box-sizing: border-box;
        }
        .logo-area { text-align: center; margin-bottom: 50px; }
        .logo-icon { font-size: 50px; margin-bottom: 10px; display: block; }
        .logo-title { color: #000000; margin-bottom: 5px; line-height: 1.1; }
        .title-bold { font-size: 38px; font-weight: 900; letter-spacing: -1.5px; display: block; }
        .title-light { font-weight: 200; font-size: 20px; display: block; margin-top: 2px; }
        .logo-sub { font-size: 15px; color: #888; margin-top: 15px; }

        .login-group { width: 100%; display: flex; flex-direction: column; gap: 15px; }
        .login-btn {
            width: 100%; height: 55px; border-radius: 12px; border: none;
            display: flex; align-items: center; justify-content: center;
            font-size: 16px; font-weight: bold; cursor: pointer; transition: 0.2s;
        }
        .btn-kakao { background-color: #FEE500; color: #3c1e1e; }
        .btn-google { background-color: #ffffff; color: #757575; border: 1px solid #ddd; }
        .login-btn:active { transform: scale(0.98); opacity: 0.9; }

        /* 요청하신 화이트 폰트 스타일 */
        .info-text { margin-top: 30px; font-size: 12px; color: #999; text-align: center; line-height: 1.6; }
        .highlight { color: white; background-color: #333; padding: 2px 6px; border-radius: 4px; }
    </style>
</head>
<body>
    <div class="mobile-container">
        <div class="logo-area">
            <span class="logo-icon">⚖️</span>
            <div class="logo-title">
                <span class="title-bold">내탓네탓</span>
                <span class="title-light">: 이게 내 잘못이야?</span>
            </div>
            <div class="logo-sub">억울한 마음, 시원한 판결</div>
        </div>

        <div class="login-group">
            <button class="login-btn btn-kakao" onclick="handleLogin('kakao')">
                카카오로 시작하기
            </button>
            <button class="login-btn btn-google" onclick="handleLogin('google')">
                구글로 시작하기
            </button>
        </div>

        <p class="info-text">
            로그인 시 이용약관 및 개인정보 처리방침에 동의하게 되며,<br>
            서비스 분석을 위해 <span class="highlight">나이와 성별</span> 정보를 수집합니다.
        </p>
    </div>

    <script>
        function handleLogin(platform) {
            const mockSocialId = platform + "_user_12345";
            let allUsers = JSON.parse(localStorage.getItem('registeredUsers') || '{}');
            
            if (allUsers[mockSocialId]) {
                alert("반가워요! 다시 오셨군요.");
                localStorage.setItem('currentUser', JSON.stringify(allUsers[mockSocialId]));
                
                // 1. 뒤로가기 방지를 위해 replace 사용
                location.replace('main.html'); 
            } else {
                alert("신규 가입을 환영합니다! 가입 처리를 완료합니다.");
                
                // 금색 코인 규칙 적용: 질문(100), 재심(300) [cite: 2026-01-29]
                const newUser = {
                    id: mockSocialId,
                    platform: platform,
                    joinDate: new Date().toISOString(),
                    coins: 1000 // 초기 코인 설정 (예시)
                };
                
                allUsers[mockSocialId] = newUser;
                localStorage.setItem('registeredUsers', JSON.stringify(allUsers));
                localStorage.setItem('currentUser', JSON.stringify(newUser));
                
                // 2. 뒤로가기 방지를 위해 replace 사용
                location.replace('main.html');
            }
        }
    </script>
</body>
</html>
