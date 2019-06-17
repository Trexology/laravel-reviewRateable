<?php

use Illuminate\Database\Schema\Blueprint;
use Illuminate\Database\Migrations\Migration;

class CreateRatingsTable extends Migration
{
    public function up()
    {
        Schema::create('ratings', function (Blueprint $table) {
            $table->increments('id')->unsigned();
            $table->double('rating');
            $table->string('title');
            $table->text('body')->nullable();
            $table->boolean('anonymous')->default(false);
            $table->morphs('reviewrateable');
            $table->morphs('author');
            $table->softDeletes();
            $table->timestamps();
        });
    }

    public function down()
    {
        Schema::dropIfExists('ratings');
    }
}
