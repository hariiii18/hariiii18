# 必要なモジュールをimport
import requests
import json
import pandas as pd
import os
import sys
import re
from datetime import datetime as dt
from dotenv import load_dotenv

def main():
    '''
    メイン関数
    '''

    # .envファイルからトークン情報などの取得
    load_dotenv()
    # os.environ.getまたはos.getenvを使用してenvファイルからトークン情報の読み込み
    access_token = os.getenv("ACCESS_TOKEN")
    version = os.getenv("VERSION")
    ig_user_id = os.getenv("IG_USER_ID")
    # ユーザーIDを入力
    user_id = "mr.cheesecake.tokyo"
    # 今日の日付を取得　文字列で年-月-日の型式にする
    today = dt.now().strftime('%y-%m-%d')
    # ユーザーIDを使ってビジネスディスカバリー情報の取得
    account_dict = call_business_profile(version, ig_user_id, user_id, access_token)
    print(account_dict)
    # API制限に引っかかった場合の処理　account_dict['error']['code'] == 4となる場合

    # 取得した情報をjson_normalizeで一気にデータフレーム型式に変換

    # 重複したカラム名があるとデータポータルで読み込めないため、重複しているカラム名idの左側のほうを残して右側は削除

    # メディア情報の取り出し

    # データフレームを作るための空の辞書を作成

    # after_keyがあれば、追加でデータを取得

    # after_keyがある場合

    # 追加でデータを取得する

    # concatを使って先に作成したデータフレームと結合する

    # インデックスを振りなおす

    # 結果csv保存用のディレクトリ作成

    # after_keyがない場合　そのままデータフレームを作成

    """
    結果データ保存のための
    ディレクトリ作成
    """

    """
    データフレームのデータを
    入れるための辞書の作成
    """

    # 空の辞書を作成　pd.DataFrame(dict)すればデータフレームが簡単にできる

    # データフレームにするカラム名をキーとして、空のリストで初期化


def call_business_profile(version, ig_user_id, user_id, access_token):
    """
    ビジネスディスカバリーで
    アカウントのプロフィール情報を取得
    """
    # ビジネスディスカバリーのエンドポイントの設定　"https://graph.facebook.com/v9/ig_user_id?fields=business_discovery.username(user_id)){followers_count,media_count,media{comments_count,like_count}}&access_token={access-token}"
    business_api = f'https://graph.facebook.com/{version}/{ig_user_id}?fields=business_discovery.username({user_id}){{username, website, name, id, profile_picture_url, biography, follows_count, followers_count, media_count, media{{timestamp, like_count, comments_count, caption, media_url}}}}&access_token={access_token}'
    # GETリクエスト
    r = requests.get(business_api)
    # JSON文字列を辞書に変換
    account_dict = json.loads(r.content)
    return account_dict


'''
ページ送りのafter_keyを取得する
'''

# after_keyがある場合

# after_keyがない場合

'''
ユーザー名とafter_keyを受け取り、追加データ分を
再度ビジネスディスカバリーでデータを取得する
'''
# ビジネスディスカバリーのページ送りのエンドポイントの設定　"https://graph.facebook.com/v9/ig_user_id?fields=business_discovery.username(user_id)){media.after(after_key).limit(number)followers_count,media_count,media{comments_count,like_count}}&access_token=access-token"

# JSON文字列を辞書に変換

"""
データフレームの作成
キーがない場合もあるので、
try-exceptでエラー処理を記述
"""

# まず要素を取り出す media_url、caption、hash_tags、timestamp、like_count、comments_count

# data_dictの各リストにappendで要素を入れていく

# たまにキーがない場合があるので、その場合の処理を記述

# まず要素を取り出す media_url、caption、hash_tags、timestamp、like_count、comments_count

# data_dictの各リストにappendで要素を入れていく

