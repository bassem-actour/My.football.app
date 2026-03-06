<script>
    const API_KEY = 'a6af9837cb044608bb0451338f417fa8'; 
    const URL = 'https://api.football-data.org/v4/matches';

    async function getLiveMatches() {
        try {
            const response = await fetch(URL, {
                headers: { 'X-Auth-Token': API_KEY }
            });
            const data = await response.json();
            
            const container = document.getElementById('matches-container');
            if (!data.matches || data.matches.length === 0) {
                container.innerHTML = '<p style="text-align:center">لا توجد مباريات مجدولة اليوم</p>';
                return;
            }

            container.innerHTML = ''; 

            data.matches.forEach(match => {
                // تحديد الحالة بالعربية بشكل أدق
                let statusText = 'قريباً';
                if (match.status === 'IN_PLAY') statusText = '● مباشر';
                if (match.status === 'FINISHED') statusText = 'انتهت';

                // معالجة النتيجة (إذا كانت null تظهر كـ 0)
                const hScore = match.score.fullTime.home ?? 0;
                const aScore = match.score.fullTime.away ?? 0;

                container.innerHTML += `
                    <div class="match-card">
                        <div class="team-box">
                            <img src="${match.homeTeam.crest}" width="30" height="30" onerror="this.src='https://via.placeholder.com/30?text=?'">
                            <span class="team-name">${match.homeTeam.shortName || match.homeTeam.name}</span>
                            <span class="score">${hScore}</span>
                        </div>
                        <div class="match-center">
                            <div class="live-indicator" style="color: ${match.status === 'IN_PLAY' ? 'red' : '#777'}">${statusText}</div>
                            <span class="game-time">${new Date(match.utcDate).toLocaleTimeString('ar-EG', {hour: '2-digit', minute:'2-digit'})}</span>
                        </div>
                        <div class="team-box">
                            <span class="score">${aScore}</span>
                            <span class="team-name">${match.awayTeam.shortName || match.awayTeam.name}</span>
                            <img src="${match.awayTeam.crest}" width="30" height="30" onerror="this.src='https://via.placeholder.com/30?text=?'">
                        </div>
                    </div>
                `;
            });
        } catch (error) {
            console.error("خطأ في الاتصال:", error);
            document.getElementById('matches-container').innerHTML = '<p style="text-align:center; color:red;">حدث خطأ أثناء جلب البيانات</p>';
        }
    }

    getLiveMatches();
    setInterval(getLiveMatches, 120000);
</script>
