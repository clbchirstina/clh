API利用できない
curl -X POST https://www.clubhouseapi.com/api/start_phone_number_auth \
  -H "Content-Type: application/json" \
  -H "CH-Languages: ja-JP" \
  -H "CH-Locale: ja_JP" \
  -H "CH-AppVersion: 0.1.27" \
  -H "CH-AppBuild: 304" \
  -d '{"phone_number": "+81"}'

URLから情報取得
手順：

Clubhouse のプロフィールページを開く

例：https://www.clubhouse.com/@eddiem13


開発者ツールを開く

Windows: F12 または Ctrl + Shift + I
Mac: Cmd + Option + I


Console タブをクリック
以下のコードを貼り付けて Enter：

// JavaScript
(function() {
  try {
    // __NEXT_DATA__ からデータを取得（最も確実）
    const nextData = JSON.parse(document.getElementById('__NEXT_DATA__').textContent);
    const routeProps = nextData.props.pageProps.routeProps;
    const userProfile = routeProps.user;
    
    // メタデータから説明を取得
    const metaDescription = document.querySelector('meta[name="description"]')?.content || userProfile.bio;
    
    const clubhouseData = {
      name: userProfile.full_name,
      username: '@' + userProfile.username,
      bio: metaDescription,
      avatar: userProfile.photo_url,
      followers: routeProps.num_followers || 0,
      following: routeProps.num_following || 0,
      friends: routeProps.friend_count || 0,
      category: 'その他',
      url: window.location.href.split('?')[0]
    };
    
    copy(JSON.stringify(clubhouseData, null, 2));
    
    console.log('✅ データをクリップボードにコピーしました!');
    console.log('━━━━━━━━━━━━━━━━━━━━━━━━━━━');
    console.log('📋 取得したデータ:');
    console.table(clubhouseData);
    console.log('━━━━━━━━━━━━━━━━━━━━━━━━━━━');
    
    // 成功通知を表示
    alert(`✅ データをコピーしました!\n\n名前: ${clubhouseData.name}\nユーザー名: ${clubhouseData.username}\nフォロワー: ${clubhouseData.followers.toLocaleString()}\n\n管理ページで「🔗 URLから追加」→「インポート」してください。`);
    
    return clubhouseData;
    
  } catch (error) {
    console.error('❌ エラー:', error);
    alert('データの取得に失敗しました。\n\nコンソールを確認してください。');
  }
})();
