# jQuery TreeGrid Extension for Yii 2

This is the [jQuery TreeGrid](https://github.com/maxazan/jquery-treegrid) extension for Yii 2. It encapsulates TreeGrid component in terms of Yii widgets,
and thus makes using TreeGrid component in Yii applications extremely easy

[![Yii2](https://img.shields.io/badge/Powered_by-Yii_Framework-green.svg?style=flat)](http://www.yiiframework.com/)
[![Latest Stable Version](https://poser.pugx.org/leandrogehlen/yii2-treegrid/v/stable.png)](https://packagist.org/packages/leandrogehlen/yii2-treegrid)
[![Total Downloads](https://poser.pugx.org/leandrogehlen/yii2-treegrid/downloads.png)](https://packagist.org/packages/leandrogehlen/yii2-treegrid)

## Installation

The preferred way to install this extension is through [composer](http://getcomposer.org/download/).

Either run

```
php composer.phar require --prefer-dist leandrogehlen/yii2-treegrid "*"
```

or add

```
"leandrogehlen/yii2-treegrid": "*"
```

to the require section of your `composer.json` file.

## How to use

**Model**

```php

use yii\db\ActiveRecord;

/**
 * @property string $description
 * @property integer $parent_id
 */
class Tree extends ActiveRecord 
{
    public $level;
    /**
     * @inheritdoc
     */
    public static function tableName()
    {
        return 'tree';
    }  
    
    /**
     * @inheritdoc
     */
    public function rules()
    {
        return [
            [['description'], 'required'],
            [['description'], 'string'],
            [['parent_id'], 'integer']
        ];
    }
}
```

**Controller**

```php
use yii\web\Controller;
use Yii;
use yii\data\ActiveDataProvider;

class TreeController extends Controller
{

    /**
     * Lists all Tree models.
     * @return mixed
     */
    public function actionIndex()
    {
        $query = Tree::find();
        $dataProvider = new ActiveDataProvider([
            'query' => $query,
            'pagination' => false
        ]);

        return $this->render('index', [
            'dataProvider' => $dataProvider
        ]);
    }
```

**View**

```php
use leandrogehlen\treegrid\TreeGrid;
  
<?= TreeGrid::widget([
    'dataProvider' => $dataProvider,
    'keyColumnName' => 'id',
    'parentColumnName' => 'parent_id',
    'levelColumnName' => 'level',
    'parentRootValue' => '0', //first parentId value
    'pluginOptions' => [
        'initialState' => 'collapsed',
    ],
    'columns' => [
        'name',
        'level',
        'id',
        'parent_id',
        ['class' => 'yii\grid\ActionColumn']
    ]     
]); ?>
```
