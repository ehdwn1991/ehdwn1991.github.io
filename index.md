<html lang="ko">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Redirecting...</title>
    <script>
        let count = 5;
        function countdown() {
            document.getElementById('countdown').innerText = count; // 초기값 표시
            if (count > 0) {
                setTimeout(() => {
                    count--;
                    countdown();
                }, 1000);
            } else {
                window.location.href = "https://codex-devlab.github.io/";
            }
        }

        window.onload = function() {
            countdown();
            let video = document.getElementById("redirect-video");
            video.playbackRate = 2; // 🎬 1.5배속 설정
        };
    </script>
</head>
<body style="text-align: center; font-family: Arial, sans-serif;">
    <h2>Jekyll을 떠나...</h2>
    <h2>새로운 블로그로 이동 합니다...</h2>
    
    <!-- 🎬 MP4 비디오 자동 재생 -->
    <video id="redirect-video" width="640" height="480" autoplay loop muted>
        <source src="https://ehdwn1991.github.io/assets/img/nodding.mp4" type="video/mp4">
        브라우저가 영상을 지원하지 않습니다.
    </video>

    <p><strong><span id="countdown">5</span>초 후에 자동으로 이동합니다.</strong></p>
    <p>만약 자동으로 이동되지 않으면 <a href="https://codex-devlab.github.io/">여기를 클릭하세요</a>.</p>
</body>
</html>
