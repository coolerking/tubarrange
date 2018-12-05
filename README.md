# tubclean 直後の tubデータ再整理ツール

[Donkey Car]() にて提供されている`donkey`コマンドの`tubclean`を実行すると、編集により削除した連番が崩れ、削除した箇所が縞状になります。
このままでは`makemovie`や`tubhist`だけでなく、`python manage.py train ..`でもエラーとなってしまいます。

この連番は単に0から順番に詰め直すだけでは整理できません。`record_連番.json`内の`cam/image_array`値にイメージファイル名(例：`連番_cam-image_array_.jpg`)が格納されているので、JSONファイルも更新しなくてはなりません。

本ツールは、引数`--tub`指定されたディレクトリ内のtubデータを読み取り、連番を再構成しJSONファイルもすべて書き直して、引数`--data`で指定されたディレクトリへ`meta.josn`含めコピー・更新します。
```bash
# ./tub 上のすべてのtubデータを再構成して ./data へコピー・更新する
python tubarrange.py --tub tub --data data
```

なお、引数指定しない場合、`./tub`ディレクトリから、`./data`ディレクトリへコピー・更新します。
```bash
# ./tub 上のすべてのtubデータを再構成して ./data へコピー・更新する
python tubarrange.py
```

デフォルトではメッセージを表示しないので、大量のデータを処理する場合(15分から20分手動走行したデータなど)、処理しているのかどうかわかりません。処理内容を表示する場合は`--debug`オプションをつけてください。
```bash
# コンソールのスクロールが遅い場合は、以下の様の実行します。
python tubarrange.py --tub tub_20XXMMDD --data data_20XXMMDD --debug > logs/tubarrange_20XXMMDD.log &
tail -f logs/tubarrange_20XXMMDD.log
```

## 注意事項

- コピー先ディレクトリは存在しなくてもOKですが、なにかファイルが１つでも存在するとExceptionをスローします
- コピー元にtubデータ以外のファイルが存在する場合は、無視されます


## ライセンス

本リポジトリの上記OSSで生成、コピーしたコード以外のすべてのコードは[MITライセンス](./LICENSE)準拠とします。




