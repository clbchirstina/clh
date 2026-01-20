API利用できない
curl -X POST https://www.clubhouseapi.com/api/start_phone_number_auth \
  -H "Content-Type: application/json" \
  -H "CH-Languages: ja-JP" \
  -H "CH-Locale: ja_JP" \
  -H "CH-AppVersion: 0.1.27" \
  -H "CH-AppBuild: 304" \
  -d '{"phone_number": "+81"}'
