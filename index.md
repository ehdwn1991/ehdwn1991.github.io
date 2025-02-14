<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Redirecting...</title>
    <script>
        let count = 5;
        function countdown() {
            if (count > 0) {
                document.getElementById('countdown').innerText = count;
                count--;
                setTimeout(countdown, 1000);
            } else {
                window.location.href = "https://codex-devlab.github.io/";
            }
        }

        window.onload = function() {
            countdown();
            let video = document.getElementById("redirect-video");
            video.playbackRate = 1.5; // 🎬 재생 속도 1.5배
        };
    </script>
</head>
<body style="text-align: center; font-family: Arial, sans-serif;">
    <h2>새로운 블로그로 이동 중...</h2>
    
    <!-- 🎬 MP4 비디오 자동 재생 -->

    <video id="redirect-video" width="320" height="240" autoplay loop muted>
        <source src="https://ehdwn1991.github.io/assets/img/nodding.mp4" type="video/mp4">
        브라우저가 영상을 지원하지 않습니다.
    </video>

    <p><strong><span id="countdown">3</span>초 후에 자동으로 이동합니다.</strong></p>
    <p>만약 자동으로 이동되지 않으면 <a href="https://codex-devlab.github.io/">여기를 클릭하세요</a>.</p>
</body>
</html>
