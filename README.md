# sensei-no-atorie-ubuntu                                       
                                                                  
  先生のアトリエ（AI授業活動設計ツール）をUbuntu実機サーバーで動かすための構築記録です。                                          
                                                                
  ## 概要                                                         
   
  Vercel Serverless Functionsで動いていたアプリを、自宅のDynabookにUbuntu + Nginx + Express + PM2 + Redis の構成で移植しました。    
                                                                  
  ## 構成
                                                                  
  クライアント（ブラウザ）                                      
      ↓                                  
  Nginx（リバースプロキシ / ポート80）        
      ↓                                   
  Express（Node.js / ポート3000）
      ├── Redis（レート制限：1日5回）                             
      └── Gemini API（授業活動の生成）        
                                                                  
  ## Vercel版との比較                                           
                                                                  
  | 項目 | Vercel版 | Ubuntu版 |
  |---|---|---|                                                   
  | サーバー | Vercel Serverless | Nginx + Express |            
  | プロセス管理 | Vercel | PM2 |             
  | レート制限ストア | Upstash Redis | Redis（ローカル） |
  | 環境変数 | Vercel管理 | .env（dotenv） |  
                                                                  
  ## ファイル構成
                                                                  
  sensei-no-atorie-ubuntu/                                      
  ├── server.js          # Expressサーバー本体                  
  ├── api/                                                      
  │   └── generate.js    # Gemini API呼び出し・レート制限
  └── package.json
                                                                  
  ## 手動テスト結果
                                                                  
  | テスト項目 | 結果 |                                         
  |---|---|                               
  | Redis疎通確認 | OK |
  | APIの応答確認 | OK |                                          
  | レート制限（5回超で429） | OK |
                                                                  
  ## 環境変数                                                   
                                          
  .env.example を参照してください。
